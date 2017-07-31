# Prepending Container configuration

A Contao *Managed Edition* does not include a default Symfony configuration.
All container configuration must be loaded by the plugins requiring a bundle.


## How it's done

Implement ``Contao\ManagerPlugin\Config\ConfigPluginInterface`` in your Manager
Plugin and specify the config files to be loaded:

```php
namespace Vendor\ContaoSomething\ContaoManager;

use Contao\ManagerPlugin\Config\ConfigPluginInterface;

class ContaoManagerPlugin implements ConfigPluginInterface
{
    /**
     * {@inheritdoc}
     */
    public function registerContainerConfiguration(LoaderInterface $loader, array $managerConfig)
    {
        $loader->load(__DIR__ . '/../Resources/custom-config1.yml');
        $loader->load(__DIR__ . '/../Resources/custom-config2.yml');
    }
}
```

> TODO: What's the ``$managerConfig`` array for?


## Best practice
You should always specify a default config your bundle is able to run with.
Otherwise installing your bundle within a fully managed environment like the
*Contao Managed Edition* together with the *Contao Manager* would lead to a
case where the user again would have to edit config files to make it run
(which is somehow opposed to the idea of a managed environment).
 
Of course there are scenarios where a user set parameter is crucial (like for
example the api key in a Twitter integration). Here it's best practice to...  

> TODO: Will the Contao Manager allow editing yml configs? What's the best practice?
>       Should a developer till then still use ``tl_config`` for things a site admin
>       should be able to change?


## Examples

To find out more have a look how some of the Contao default bundles implement
this interface:

 * The [Manager Plugin of the ``ManagerBundle``][ex1] loads Contao's default
   config files for the *Managed Edition* to work.
 

 
[ex1]: https://github.com/contao/manager-bundle/blob/4.4.2/src/ContaoManager/Plugin.php#L80-L97