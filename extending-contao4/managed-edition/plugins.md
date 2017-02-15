# Introduction to Contao Manager Plugins

Manager Plugins are the main entry point to add custom features to the
Contao *Managed Edition*. 

> #### info:: Note
> This describes `contao/manager-plugin` version 2.0.


## The interfaces

A plugin should be a standalone class, its features are described by
implementing different interfaces.

More interfaces will likely be added in the future when new features are
added to Contao or the Contao Manager.


### BundlePluginInterface

The `Contao\ManagerBundle\ContaoManager\Bundle\BundlePluginInterface`
allows a plugin to load bundles into the Symfony kernel at boot time.

This method is usually implemented by a Composer package to load its
Symfony bundle and dependencies.

* [Autoloading Contao 4 / Symfony bundles](bundle-autoloading.md)


### ConfigPluginInterface

The `Contao\ManagerBundle\ContaoManager\Config\ConfigPluginInterface` allows
a plugin to register container configuration at build time. This is smiliar
to prepending configuration in Symfony, but it is only executed
in a Contao *Managed Edition* application.

* [Container configuration](container-configuration.md)


### RoutingPluginInterface

The `Contao\ManagerBundle\ContaoManager\Routing\RoutingPluginInterface`
enables a plugin to register custom routes for the Symfony router.

* [Adding routes](routing.md)


### DependentPluginInterface

Some features, like prepending routing configuration, require a specific order
of plugins to correctly override each other. If your plugins needs to override
a route of another plugin, it must be loaded before that.

The `Contao\ManagerBundle\ContaoManager\Dependency\DependentPluginInterface`
allows to define a list of **Composer packages** whose plugins must be loaded
before the current plugin.

* [Defining plugin dependencies](plugin-dependencies.md)


## Working with the plugin

If you're developing a Contao 4 bundle, it is recommended to add a
manager plugin to enable installation in a Contao *Managed Edition*.
The setup is fairly simple.


### Class and Namespace

Create a plugin class in your bundle. The best practice is to create
a `Plugin` class in a `ContaoManager` folder/subnamespace. The result
would be a class like `Vendor\SomeBundle\ContaoManager\Plugin`.

This class can then implement any of the available interfaces to
work with the Contao *Managed Edition*.


### composer.json

Each Composer package can have one plugin, and it must be registered
in the *composer.json*.

1. Add a node `contao-manager-plugin` in the [`extra` section][1]. The
   result will look something like this:

    ```json
    {
       "extra": {
            "contao-manager-plugin": "Vendor\\SomeBundle\\ContaoManager\\Plugin"
       }
    }
    ```

2. Add the plugin to your dev requirements:

    ```json
    {
       "require-dev": {
            "contao/manager-plugin": "^2.0"
       }
    }
    ```

3. Because the plugin is only a dev requirement, it will not affect
   a regular installation of packages. You need to add a conflict to
   make sure it's only installed in a compatible setup.

    ```json
    {
       "conflict": {
            "contao/manager-plugin": "<2.0 || >=3.0"
       }
    }
    ```

[1]: https://getcomposer.org/doc/04-schema.md#extra
