# Autoloading Contao 4 or Symfony bundles

Contao 4 is a full-featured Symfony application. Extending a Symfony application
is accomplished using so-called *bundles*, which can extend the configuration
at compilation-time. [Read more](http://symfony.com/doc/current/bundles.html) 
about bundles in the Symfony manual.

Because Contao *Managed Edition* does not know what bundles exist and in what
order they must be loaded, the Manager Plugin needs to tell that to the 
application.


## How it's done

Implement ``Contao\ManagerPlugin\Bundle\BundlePluginInterface`` in your Manager
Plugin and specify at least one ``BundleConfig``. In a bundle config you can define
if a specific bundle should be loaded after another, should replace a legacy
one or should only be loaded in the production/development environment. 

Here is an example, that explicitly tells the system to load your bundle after
the ``ContaoCoreBundle``, ``TwigBundle`` and ``ContaoManagerBundle``:

```php
namespace Vendor\ContaoSomething\ContaoManager;

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
            BundleConfig::create(VendorContaoSomethingBundle::class)
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

> TODO: What's the ``ParserInterface`` for other than autoloading a Contao 3
>       ``autload.ini``? 

> #### info:: Hint
> You can specify more than one bundle config. This way you can define
> properties for bundles that don't have an own Manager Plugin. 


## Examples

To find out more have a look how some of the Contao default bundles implement
this interface:

 * a very simple config: [Manager Plugin of the ``NewsBundle``][ex1]
 * a more advanced version with multiple bundle configs: 
   [Manager Plugin of the ``CoreBundle``][ex2]
 

 
[ex1]: https://github.com/contao/news-bundle/blob/4.4.2/src/ContaoManager/Plugin.php#L29-L36
[ex2]: https://github.com/contao/core-bundle/blob/4.4.2/src/ContaoManager/Plugin.php#L44-L692