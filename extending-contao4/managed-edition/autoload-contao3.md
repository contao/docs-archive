# Autoloading Contao 3 extensions

To make a Contao 3 extension available in Contao *Managed Edition*, it needs
to fulfill two prerequisites:

1. Be available through Composer (usually on [Packagist])
2. Include a Contao Manager Plugin


## Enabling Composer support

To add Composer compatibility to a Contao 3 extension, you must follow the
information for the [Contao Composer Plugin].


## Create a Manager Plugin

Create a Manager Plugin described in the [respective section](plugins.md).


### Load dependencies from `autoload.ini`

Usually, a Contao 3 extension comes with a `config/autoload.ini` file to 
describe it's dependencies, which is automatically parsed in Contao 3. 
In Contao 4, the plugin must load the dependencies from this file by 
implementing the `BundlePluginInterface` and using the parser to recursively 
load all dependencies.

Optional dependencies (prefixed with `*`) still work in Contao 4, if a module
folder does not exist that dependency is simply skipped.


#### Example:

```php
namespace Vendor\MyModule\ContaoManager;

use Contao\ManagerBundle\ContaoManager\Bundle\BundlePluginInterface;
use Contao\ManagerBundle\ContaoManager\Bundle\ParserInterface;

class Plugin implements BundlePluginInterface
{
    public function getBundles(ParserInterface $parser)
    {
        return $parser->parse('my-module-name', 'ini');
    }
}
```


> #### info:: Note
> Contao 4 bundles will automatically provide conversion for old module names
> to new Symfony bundles (e.g. *core* equals *ContaoCoreBundle* now).
> You must not change your `autoload.ini` or it will no longer work in Contao 3.


### Other plugin features

The other features available for Manager Plugins do not make much sense to use
for a Contao 3 extension, as they will not be supported in Contao 3.



[Packagist]: https://packagist.org
[Contao Composer Plugin]: https://github.com/contao-community-alliance/composer-plugin/blob/master/README.md
