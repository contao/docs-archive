# Adjusting the configuration of other bundles

> #### primary:: Available
> from Contao _Managed Edition_ 4.4.


The easiest way to define bundle configuration is by using the
[ConfigPluginInterface](container-configuration.md). It allows to register
any bundle configuration, for the current bundle or any third party one.

This works in _most_ of the cases. The Symfony ContainerBuilder simply performs
a recursive array merge operation of all configurations. The result is:

1. Plugin configuration is loaded before the global config
   (`app/config/config.yml`), therefore the global config can override bundles.

2. Plugin configuration is loaded (and overridden) in order of the plugins.
   One plugin can override the bundle configuration set by another plugin
   by setting the same keys. The order of plugins can be adjusted using the
   [DependendPluginInterface](plugin-dependencies.md).

3. When merging configurations with multiple nodes (like `doctrine.dbal.connections`,
   `framework.cache.pools`), the nodes are simply merged. This is usually not a problem,
   because database connections etc. are named, so the order in the tree does not matter.

4. If the order of configuration matters (e.g. `security.firewalls`,
   `monolog.handlers`), it can be hard to get right. Also, some nodes prohibit
   merging (using [`disallowNewKeysInSubsequentConfigs()`][1]) which results
   in an exception if two plugins trie to set the same configuration.


The `ExtensionPluginInterface` is **only** meant and necessary to work around
the issues mentioned in point 4.


## Examples

### Adding a custom Symfony Firewall

A typical example for overriding previous bundle configuration would be the
`security.firewalls` configuration. You might want to configure another firewall
than the one Contao ships by default. As you know, the order matters because the
first firewall that matches a specific pattern or request is the one that Symfony
is going to use. That's why you cannot simply have a `config.yml` with your own
`security.firewalls` configuration – the Symfony Config component will tell you:

> You are not allowed to define new elements for path "security.firewalls".

Symfony makes sure that `security.firewalls` is specified only once. This is the
only way it can ensure the order of firewalls is correct.

Thanks to the `Contao\ManagerBundle\ContaoManager\Config\ExtensionPluginInterface`
you can, however, modify the all extension configurations of all the other bundles
**before** that check is executed.

Here's an example of how you could add your own firewall in front of the Contao
`frontend` firewall:

```php
<?php

namespace Vendor\MyBundle\ContaoManager;

use Contao\ManagerPlugin\Config\ContainerBuilder;
use Contao\ManagerPlugin\Config\ExtensionPluginInterface;

class Plugin implements ExtensionPluginInterface
{
    /**
     * Allows a plugin to override extension configuration.
     *
     * @param string           $extensionName
     * @param array            $extensionConfigs
     * @param ContainerBuilder $container
     *
     * @return array
     */
    public function getExtensionConfig($extensionName, array $extensionConfigs, ContainerBuilder $container)
    {
        if ('security' !== $extensionName) {
            return $extensionConfigs;
        }

        foreach ($extensionConfigs as &$extensionConfig) {
            if (isset($extensionConfig['firewalls'])) {
                
                // Add e.g. your own security authentication provider
                $extensionConfig['providers']['app.api_user_provider'] = [
                    'id' => 'app.security.api_user_provider'
                ];
                
                // Add your own firewall before the "frontend" firewall of Contao
                // Int-Cast position so "false" (not found) results in position 0.
                $offset = (int) array_search('frontend', array_keys($extensionConfig['firewalls']));
                
                $extensionConfig['firewalls'] = array_merge(
                    array_slice($extensionConfig['firewalls'], 0, $offset, true),
                    [
                        'api' => [
                            'pattern' => '/api/*',
                            'anonymous' => true,
                            'guard' => [
                                'authenticators' => [
                                    'app.security.api_guard_authenticator'
                                ],
                            ],
                        ],
                    ],
                    array_slice($extensionConfig['firewalls'], $offset+1, null, true)
                );
                
                break;
            }
        }

        return $extensionConfigs;
    }
}
```

Note that you receive an array of `$extensionConfigs` and you may have to apply
your changes multiple times. This is because of the way the Symfony Dependency
Injection Container works. E.g. you have a configuration from `config.yml` one
from "Bundle X" and another one from "Bundle Y". The container then merges all
these configurations into one (which is exactly where that firewall error message
comes from). Unfortunately, there is no way you can determine where a certain
configuration is coming from.


### Allow a clickjacking path for NelmioSecurityBundle

Another example where order matters might be the `nelmio_security.clickjacking.paths`
configuration. The reason there is the same: the rules of the first path that matches
are going to be applied. So to make sure that `/external` is allowed, your plugin
could look like this:

```php
<?php

namespace Vendor\MyModule\ContaoManager;

use Contao\ManagerPlugin\Config\ContainerBuilder;
use Contao\ManagerPlugin\Config\ExtensionPluginInterface;

class Plugin implements ExtensionPluginInterface
{

    /**
     * Allows a plugin to override extension configuration.
     *
     * @param string           $extensionName
     * @param array            $extensionConfigs
     * @param ContainerBuilder $container
     *
     * @return array
     */
    public function getExtensionConfig($extensionName, array $extensionConfigs, ContainerBuilder $container)
    {
        if ('nelmio_security' !== $extensionName) {
            return $extensionConfigs;
        }

        $customCors = [
            '^/external.*' => 'ALLOW'
        ];

        foreach ($extensionConfigs as &$extensionConfig) {

            if (isset($extensionConfig['clickjacking'])
                && is_array($extensionConfig['clickjacking']['paths'])
            ) {
                $extensionConfig['clickjacking']['paths'] = $customCors + $extensionConfig['clickjacking']['paths'];
            }
        }

        return $extensionConfigs;
    }
}

```

[1]: http://api.symfony.com/master/Symfony/Component/Config/Definition/Builder/ArrayNodeDefinition.html#method_disallowNewKeysInSubsequentConfigs
