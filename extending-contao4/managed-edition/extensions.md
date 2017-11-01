# Adjusting the configuration of other bundles

One fundamental issue with a "managed edition" is that bundles want to adjust
configuration and sometimes a simple merge of this configuration is not possible
because the order of certain keys matters. A typical example would be the
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

namespace Vendor\MyModule\ContaoManager;

use Contao\ManagerPlugin\Config\ContainerBuilder;
use Contao\ManagerPlugin\Config\ExtensionPluginInterface;

class ContaoManagerPlugin implements ExtensionPluginInterface
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
           // Add e.g. your own security authentication provider
           if (isset($extensionConfig['providers'])) {
               $extensionConfig['providers']['app.webservice_user_provider'] = [
                   'id' => 'app.security.webservice_user_provider'
               ];
           }

           // Add your own firewall before the "frontend" firewall of Contao
           if (isset($extensionConfig['firewalls'])) {
               $i = 0;
               foreach ($extensionConfig['firewalls'] as $firewall => $firewallConfig) {
                   if ('frontend' === $firewall) {
                       $appFirewall = ['app_firewall' => [
                          'pattern' => '/*',
                          'anonymous' => true,
                          'guard' => [
                              'authenticators' => [
                                  'app.security.webservice_guard_authenticator'
                              ]
                          ],
                       ]];

                       $extensionConfig['firewalls'] = array_slice($extensionConfig['firewalls'], 0, $i, true)
                           + $appFirewall
                           + array_slice($extensionConfig['firewalls'] , 3, count($extensionConfig['firewalls']) - 1, true)
                       ;
                   }

                   $i++;
               }
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

Another example where order matters might be the `nelmio_security.clickjacking.paths`
configuration. The reason there is the same: the rules of the first path that matches
are going to be applied. So to make sure that `/external` is allowed, your plugin
could look like this:

```php
<?php

namespace Vendor\MyModule\ContaoManager;

use Contao\ManagerPlugin\Config\ContainerBuilder;
use Contao\ManagerPlugin\Config\ExtensionPluginInterface;

class ContaoManagerPlugin implements ExtensionPluginInterface
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
