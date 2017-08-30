# Handling custom routes

Symfony has powerful routing capabilities that map a certain request (say some
URL) to a ``Controller`` handling it. Make your self familiar with the overall
concept of routing first: 

 → [Routing in Symfony][SymfonyRouting]
 
Every single regular requests goes through the same entry point (``app.php``)
which allows you to have full control on how your URLs look like independently
of your file structure.



## Redirects

*In some cases you even do not have to write your own custom ``Controller`` to
handle a ``Request``. Take this example that explains how some simple redirects
can be achieved to get a first idea.*

In some cases it might be helpful to define permanent redirects, for instance
for old urls that are still cached by search engines. As there is a single entry
point for regular requests, this can be achieved by adding custom routes.

> #### info:: Sidenote
> Keep in mind that legacy redirects might better be done on the web server
> side if this works in your case.


Assume you have the following old urls…

     http://yourdomain.com/old/abc/def
     http://yourdomain.com/old/app?id=123
     http://yourdomain.com/old/index.php

…and you want them to be redirected to.

    http://yourdomain.com/

Then you could add a new route (here called ``legacy_redirect``) that matches
those paths (e.g. ``/old/{anything}``) and use the already existing generic
``FrameworkBundle:Redirect:redirect`` controller where you specify the new
route to redirect to (here: ``contao_root``), whether to ignore attributes and
whether the redirect should be permanent (301).

```yml
# app/config/routing.yml

legacy_redirect:
    path: /old/{anything}
    defaults:
        _controller: FrameworkBundle:Redirect:redirect
        route: contao_root
        ignoreAttributes: true
        permanent: true
```

If you want to use *paths* instead of *routes* you have a look into
``FrameworkBundle:Redirect:urlRedirectAction``. Of course more complex url
mappings can be done by writing your [own controller][SymfonyControllers] to
handle your legacy routes.


## Custom routes in a *Managed Edition*

If you want to add custom routes inside a Contao *Managed Edition*, you can
follow these steps in which we create a global ``ContaoManagerPlugin`` and in
that load a custom routing file. 

We are using the following directory structure in this example:

    <webroot>
      ├─ app
      │   ├─ config
      │   │   ├─ config.yml
      │   │   ├─ parameters.yml
      │   │   └─ routing.yml                                
      │   └─ ContaoManagerPlugin.php                                              
      ├─ ...
      └─ composer.json


1. Add the ``routing.yml`` with your mappings to your config directory (see
   structure above). If you instead do want to create your routes on the fly,
   simply do so in the next step instead of loading the file (see [this 
   example][routeOnTheFly]). 

2. Add a new class ``ContaoManagerPlugin`` in global namespace (if you have not
   done that already) and implement the manager plugin's
   ``RoutingPluginInterface``. In the function you're therefore forced to
   implement, you can then specify where your custom routes (in your
   ``routing.yml``) can be found.

    ```php
    // app/ContaoManagerPlugin.php
    
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
                ->resolve(__DIR__ . '/config/routing.yml')
                ->load(__DIR__ . '/config/routing.yml');
        }
    } 
    ```

3. Tell the autoloader where to find the global ``ContaoManagerPlugin`` by
   adding a classmap entry to your project's ``composer.json``:

    ```json
    // composer.json
    
    {
       [...]
    
       "autoload": {
        "classmap": [
          "app/ContaoManagerPlugin.php"
        ]
      }
   }
    ```
    
    
[SymfonyRouting]: https://symfony.com/doc/current/routing.html
[SymfonyControllers]: https://symfony.com/doc/current/best_practices/controllers.html
[routeOnTheFly]: https://github.com/contao/manager-bundle/blob/4.4.2/src/ContaoManager/Plugin.php#L133-L141