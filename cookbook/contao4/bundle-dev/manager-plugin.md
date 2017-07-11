# Manager Plugin

To make your bundle compatible with the automatic loading and configuration in the managed edition, you have to add a
``ContaoManagerPlugin.php`` where you specify how the bundle should be loaded, what possible package dependencies must
be regarded, which routes should be installed… 

## Minimal setup

1. Add a ``ContaoManagerPlugin.php`` to your bundle (e.g. in the source root):
    ```php
     namespace MyName\ContaoSomething;
             
     class ContaoManagerPlugin
     {    
     }
       
    ```
2. Add a new key ``extra`` to your bundle's ``composer.json`` that points to your just created class:
    ```json
    [...]
 
      "extra": {
        "contao-manager-plugin": "MyName\\ContaoSomething\\ContaoManagerPlugin"
      }
    ```



## Configuration

To define your setup simply implement the respective interfaces in your manager plugin (each with a function that
returns the configuration). Of course you can implement as many interfaces in parallel as you want.

### Dependent bundles loading order and more
Implement ``Contao\ManagerPlugin\Bundle\BundlePluginInterface`` in your manager plugin and specify at least one bundle
config. In a bundle config you can define if a specific bundle should be loaded after another, should replace a legacy
one or should only be loaded in the production/development environment. 

Here is an example, that explicitly tells the system to load your bundle after the ``ContaoCoreBundle``, ``TwigBundle``
and ``ContaoManagerBundle``:

```php
namespace MyName\ContaoSomething;

use Contao\ManagerPlugin\Bundle\BundlePluginInterface;
use Contao\ManagerPlugin\Bundle\Parser\ParserInterface;
use Contao\ManagerPlugin\Bundle\Config\BundleConfig;

class ContaoManagerPlugin implements BundlePluginInterface
{
    /**
     * {@inheritdoc}
     */
    public function getBundles(ParserInterface $parser)
    {
        return [
            BundleConfig::create(MyNameContaoSomethingBundle::class)
                ->setLoadAfter(
                    [
                        \Symfony\Bundle\TwigBundle\TwigBundle::class,
                        \Contao\CoreBundle\ContaoCoreBundle::class,
                        \Contao\ManagerBundle\ContaoManagerBundle::class,
                    ]
                ),
        ];
    }
}
```
Note that you can also return multiple bundle configs. This might be necessary if your bundle uses external libraries
that do not contain a manager plugin and that should be taken into account. 

**Alternative package dependencies**  
You can also specify which composer packages must be loaded before by implementing
``Contao\ManagerPlugin\Dependency\DependentPluginInterface`` and returning a list of package names from the 
``getPackageDependencies()`` function analogous to the ``getBundles()`` function. 



### Custom routes
If you want to add custom routes implement ``Contao\ManagerPlugin\Routing\RoutingPluginInterface`` and specify a routing
configuration:
```php
namespace MyName\ContaoSomething;

use Contao\ManagerPlugin\Routing\RoutingPluginInterface;
use Symfony\Component\Config\Loader\LoaderResolverInterface;
use Symfony\Component\HttpKernel\KernelInterface;

class ContaoManagerPlugin implements RoutingPluginInterface
{
    /**
     * {@inheritdoc}
     */
    public function getRouteCollection(LoaderResolverInterface $resolver, KernelInterface $kernel)
    {
        return $resolver
            ->resolve('Resources/config/routing.yml')
            ->load('Resources/config/routing.yml');
    }
} 
```


### More ###
There is more: Check out the [full documentation](../../customizing-contao/README.md).