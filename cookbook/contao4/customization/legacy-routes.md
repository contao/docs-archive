> TODO: rewrite

# Handling legacy routes

It might be helpful to define some permanent redirects for old urls that are still cached by search engines. There is a
single entry point for regular requests (``app.php``), so this problem can be solved by adding custom routes.

**Example**

Assume you have the following old urls…

     http://yourdomain.com/old/abc/def
     http://yourdomain.com/old/app?id=123
     http://yourdomain.com/old/index.php

…and you want them to be redirected to.

    http://yourdomain.com/

Then you could add a new route (here called ``legacy_redirect``) that matches those paths (e.g. ``/old/{anything}``) and
use the already existing ``FrameworkBundle:Redirect:redirect`` controller where you specify the new route to redirect to
(here: ``contao_root``), whether to ignore attributes and whether the redirect should be permanent (301).


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

If you want to use paths instead you might want to look into ``FrameworkBundle:Redirect:urlRedirectAction``. Of course 
more complex url mappings can be done by writing your 
[own controller](https://symfony.com/doc/current/best_practices/controllers.html) to handle your legacy routes.


## Setup for the managed edition

Here are the steps to get it done in the managed edition. In this example we are using the following directory
structure:


    <webroot>
      ├─ app
      │   ├─ config
      │   │   ├─ config.yml
      │   │   ├─ parameters.yml
      │   │   └─ routing.yml                                
      │   └─ ContaoManagerPlugin.php                                              
      ├─ ...
      └─ composer.json


1. Add the ``routing.yml`` with your mappings to your config directory (see example above).

2. Add a new class ``ContaoManagerPlugin`` in global namespace (if you have not done that already) and implement the
manager plugin's``RoutingPluginInterface``. In the function you're therefore forced to implement, you can then specify
where your custom routes (in your ``routing.yml``) can be found.

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

3. Tell the autoloader where to find the global ``ContaoManagerPlugin`` by adding a classmap entry to your project's
 ``composer.json``:

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