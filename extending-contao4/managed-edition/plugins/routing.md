# Routing configuration

Routing in Symfony takes care of mapping a URL to a controller.
[Read more](http://symfony.com/doc/current/routing.html) about routing in the 
Symfony manual.


## How it's done

Implement ``Contao\ManagerPlugin\Bundle\ConfigPluginInterface`` in your Manager
Plugin and specify the collection of routes you want to install.

Here is an example on how you could load a ``routing.yml`` in which you config
your routes (e.g. for a ``Controller`` you deliver with your bundle):

```php
// src/ContaoManager/Plugin.php

namespace Vendor\ContaoSomething\ContaoManager;

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
            ->resolve(__DIR__ . '/../Resources/config/routing.yml')
            ->load(__DIR__ . '/../Resources/config/routing.yml');
    }
} 
```

```yml
# src/Resources/config/routing.yml

my_custom_route:
    path: /something/{x}
    defaults:
        _controller: "VendorContaoSomethingBundle:MyController:someAction"
```

> #### info:: Hint
> You do not need to load a configuration file but can also specify the route
> directly which might be less of an overkill if you only have a few routes -
> check out the examples below to see how this could look like. 


## Loading order

The order of routes is important: In Symfony only the first matching route gets
executed. (That's for example why the ``contao_catch_all`` route from the
``CoreBundle`` must be the last one.)        

So the order in that we compose the routes is opposite to the loading order of
the bundles. Or in other words: If you specify that bundle **A** has to be
loaded *after* bundle **B**, the routes of **A** would appear *before* those of
 **B**.   


## Examples

To find out more have a look how some of the Contao default bundles implement
this interface:

 * the [Manager Plugin of the ``InstallationBundle``][ex1] just loads a ``routing.yml``
 * see how the legacy ``/install.php`` route is added in the
   [Manager Plugin of the ``ManagerBundle``][ex2]  
 


[ex1]: https://github.com/contao/installation-bundle/blob/4.4.2/src/ContaoManager/Plugin.php#L43-L49
[ex2]: https://github.com/contao/manager-bundle/blob/4.4.2/src/ContaoManager/Plugin.php#L133-L141