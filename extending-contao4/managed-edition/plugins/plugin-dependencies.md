# Plugin dependencies

For some features like [loading routes](routing.md), the order of plugins is
important for correct functionality. A plugin can define a list of 
**Composer packages** whose plugins should be loaded beforehand.

> TODO: Improve text; it should not get confused with ``BundlePluginInterface``.


## How it's done

Implement ``Contao\ManagerPlugin\Dependency\DependentPluginInterface`` in your Manager
Plugin and define the composer packages this bundle depends on:

```php
namespace Vendor\ContaoSomething\ContaoManager;

use Contao\ManagerPlugin\Dependency\DependentPluginInterface;

class ContaoManagerPlugin implements DependentPluginInterface
{
    /**
     * {@inheritdoc}
     */
    public function getPackageDependencies()
    {
        return [
            'some-vendor/composer-package',
            'another/super-library'
        ];
    }
}
```


## Examples

To find out more have a look how some of the Contao default bundles implement
this interface:

 * The [Manager Plugin of the ``ManagerBundle``][ex1] defines its dependency from the core.
 
> TODO: This is the only example that I could find. But it's not a good one (I
>       think)? This is kind of a special case here.  

 

[ex1]: https://github.com/contao/manager-bundle/blob/4.4.2/src/ContaoManager/Plugin.php#L45-L48