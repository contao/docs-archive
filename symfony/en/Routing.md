# Routing

The following chapters explain how the Symfony routing is used in Contao 4 and newer.
You will learn how to define custom static and dynamic routes and how to include third party routes.

## The routing internals

**(Hint)** If you are not interested in how the routing internally works, you can skip this chapter.

Contao use a chain router to combine static and dynamic routes. Static routes never change, e.g. the backend.
Dynamic routes are generated on demand, dependent on the current request.
For the static routing, the Symfony [routing component][_routing_component] is used.
For the dynamic routing, the CMF [dynamic router component][_cmf_dynamic_router_component] is used.

Contrary to the symfony default, static routes are not loaded through a `app/config/routing.yml` file.
Contao use its own routing loader that load routes from the bundles.
Read the chapter [Define static routes](#define-static-routes) for further informations.

The CMF dynamic router is used to generate the routes for the pages. Contao comes with its own `PageRouteProvider`
that generate the routes on demand.
Read the chapter [Define a CMF provider](#define-a-cmf-provider) for further informations.

## Custom route convention

You should always prefix your routes with `_{bundle short name}`!
Here are some examples:

* Contao: `_contao`
* Isotope: `_isotope`
* Avisota: `_avisota`
* MetaModels: `_metamodels`

Static routes are always overwrite dynamic routes. We therefore call on all developers to adhere to this convention!

## Define static routes

Define static routes for your bundle is simple. Inside your contao resources path, you have to create a
`config/routing.yml`, `config/routing.xml` or `config/routing.php` file, depending on your personal preference.
These files works the same way as the [default routing configuration][_default_routing_configuration] for Symfony.

`@AcmeContaoDemoBundle/Resources/config/routing.yml`

```yaml
acme_contao_demo_welcome:
    path:     _acme_contao_demo
    defaults: { _controller: AcmeContaoDemoBundle:Demo:index }
```

But contrary to the Symfony defaults, these routing files are automatically loaded from Contao. There is no need
to register the file in the global `app/config/routing.yml`.

**(Hint)** The automatical loading of routes only works for bundles that implement `ContaoBundleInterface`!

## Define dynamic routes

Define dynamic routes can be done in two ways.

### Define a route loader

The first and easiest way is to [create a custom route loader][_create_a_custom_route_loader].

**(Step 1)** Write your `routing.yml` as descriped in the [Define static routes](#define-static-routes) chapter.

`@AcmeContaoDemoBundle/Resources/config/routing.yml`

```yaml
AcmeContaoDemoBundle:
    resource: .
    type: acme_contao_demo_bundle
```

**(Step 2)** Write your `Loader` class.

`@AcmeContaoDemoBundle\Routing\Loader`

```php
namespace Acme\ContaoBundle\Routing;

use Symfony\Component\Config\Loader\Loader as BaseLoader;
use Symfony\Component\Routing\Route;
use Symfony\Component\Routing\RouteCollection;

class Loader extends BaseLoader
{
    private $loaded = false;

    public function load($resource, $type = null)
    {
        if (true === $this->loaded) {
            throw new \RuntimeException('Do not add the "acme_contao_demo_bundle" loader twice');
        }

        $routes = new RouteCollection();

        // prepare a new route
        $pattern = '/_acme/{parameter}';
        $defaults = array(
            '_controller' => 'AcmeContaoDemoBundle:Demo:index',
        );
        $requirements = array(
            'parameter' => '\d+',
        );
        $route = new Route($pattern, $defaults, $requirements);

        // add the new route to the route collection:
        $routeName = 'demoRoute';
        $routes->add($routeName, $route);

        $this->loaded = true;

        return $routes;
    }

    public function supports($resource, $type = null)
    {
        return 'acme_contao_demo_bundle' === $type;
    }

    public function getResolver()
    {
        // needed, but can be blank, unless you want to load other resources
        // and if you do, using the Loader base class is easier (see below)
    }

    public function setResolver(LoaderResolverInterface $resolver)
    {
        // same as above
    }
}
```

**(Step 3)** Define the loader as a service.

`@AcmeContaoDemoBundle/Resources/config/services.yml`

```yaml
services:
    acme_contao_demo.routing_loader:
        class: Acme\ContaoBundle\Routing\Loader
        tags:
            - { name: routing.loader }
```

### Define a CMF provider

The second way is to [create a cmf provider](_create_a_cmf_provider). The benefit of the CMF router is, that it is
designed to generate request specific routes.

**(Step 1)** Write your `Provider` class.

`@AcmeContaoDemoBundle\Routing\Provider`

```php
namespace Acme\ContaoBundle\Provider;

use Symfony\Cmf\Component\Routing\RouteProviderInterface;

class Provider implements RouteProviderInterface
{
    private $candidatesStrategy;

    public function __construct(CandidatesInterface $candidatesStrategy)
    {
        $this->candidatesStrategy = $candidatesStrategy;
    }

    /**
     * {@inheritdoc}
     */
    public function getRouteCollectionForRequest(Request $request)
    {
        $collection = new RouteCollection();

        $candidates = $this->candidatesStrategy->getCandidates($request);
        if (empty($candidates)) {
            return $collection;
        }
        
        // TODO: here you need to find the routes by $candidates or any custom logic

        return $collection;
    }

    /**
     * {@inheritdoc}
     */
    public function getRouteByName($name)
    {
        // TODO: here you need to find the route by $name

        return $route;
    }

    /**
     * {@inheritdoc}
     */
    public function getRoutesByNames($names = null)
    {
        $routes = array();

        if (null === $names) {
            // TODO: here you need to find all routes
            
            return $routes;
        }

        foreach ($names as $name) {
            try {
                $routes[] = $this->getRouteByName($name);
            } catch (RouteNotFoundException $e) {
                // not found
            }
        }

        return $routes;
    }
}
```

**(Step 2)** Define the loader as a service.

`@AcmeContaoDemoBundle/Resources/config/services.yml`

```yaml
services:
    acme_contao_demo.routing_provider:
        class:     Acme\ContaoBundle\Routing\Provider
        arguments:
            - '@contao.routing.candidates_strategy'
        tags:
            - { name: cmf_routing.provider }
```

**Hint** You can define a priority `{ name: cmf_routing.provider, priority: 50 }` for your provider,
this may be necessary to change the order of route generation, e.g. if you want to overwrite the default page routes.
The Contao page provider had a priority of 100.

## Include third party routes

Some third party bundles comes with their own route definition.
[Including External Routing Resources][_including_external_routing_resource] is pretty simple.
Write your `routing.yml` as descriped in the [Define static routes](#define-static-routes) chapter.
And then include the third party routing configuration file as resource.

`@AcmeContaoDemoBundle/Resources/config/routing.yml`

```yaml
AcmeContaoDemoBundle:
    resource: @ThirdPartyBundle/Resources/config/routing.yml
    prefix:   /_third_party_bundle
```

**(Hint)** You should always prefix imported routes. See chapter [Custom route convention](#custom-route-convention)
for further informations.

[_routing_component]: http://symfony.com/doc/current/components/routing/index.html
[_cmf_dynamic_router_component]: http://symfony.com/doc/master/cmf/components/routing/dynamic.html
[_default_routing_configuration]: http://symfony.com/doc/current/book/routing.html
[_create_a_custom_route_loader]: http://symfony.com/doc/current/cookbook/routing/custom_route_loader.html
[_create_a_cmf_provider]: http://symfony.com/doc/master/cmf/components/routing/nested_matcher.html#the-routeprovider
[_including_external_routing_resource]: http://symfony.com/doc/current/book/routing.html#including-external-routing-resources