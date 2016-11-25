# Introduction to Contao Manager Plugins

Manager Plugins are the main entry point to add custom features to the
Contao *Managed Edition*. 


## The interfaces

A plugin should be a standalone class, its features
are described by implementing different interfaces.

More interfaces will likely be added in the future when new features are added
to Contao or the Contao Manager.


### BundlePluginInterface

The `Contao\ManagerBundle\ContaoManager\Bundle\BundlePluginInterface` allows
a plugin to load bundles into the Symfony kernel at boot time.

This method is usually implemented by a Composer package to load its
Symfony bundle and dependencies.

* [Autoloading Contao 3 extensions](autoload-contao3.md)
* [Autoloading Contao 4 / Symfony bundles](autoload-contao4.md)


### ConfigPluginInterface

The `Contao\ManagerBundle\ContaoManager\Config\ConfigPluginInterface` allows
a plugin to prepend container configuration at build time. This works the 
same as using Symfony [configuration prepending], but it is only executed
in a Contao *Managed Edition* application.

* [Prepending Container configuration](prepend-config.md)


### RoutingPluginInterface

The `Contao\ManagerBundle\ContaoManager\Routing\RoutingPluginInterface` allows
a plugin to register custom routes for the Symfony router.

* [Adding routes](routing.md)


### DependentPluginInterface

Some features, like prepending routing configuration, require a specific order
of plugins to correctly override each other. If your plugins needs to override
a route of another plugin, it must be loaded before that.

The `Contao\ManagerBundle\ContaoManager\Dependency\DependentPluginInterface`
allows to define a list of **Composer packages** whose plugins must be loaded
before the current plugin.

* [Defining plugin dependencies](plugin-dependencies.md)



[configuration prepending]: http://symfony.com/doc/current/bundles/prepend_extension.html
