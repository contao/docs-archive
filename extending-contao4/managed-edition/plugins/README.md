# Introduction to Contao Manager Plugins

*Manager Plugins* are the main entry point to add custom features to the
*Contao Managed Edition*. 

This way you can auto configure the Managed Edition with all the things 
an application administrator typically would have to deal with manually,
think of: 
 - How should a bundle get loaded?
 - What possible package dependencies must be regarded?
 - Which custom routes must be installed?
 - What default configuration parameters must be added? 
 - … 


> #### info:: Do I need this?
> If you're developing a Contao 4 bundle, it is strongly recommended to add a
> manager plugin to enable installation in a Contao Managed Edition. Also, 
> this is a need for users to be able to install your bundle through the
> *Contao Manager*.
    
      
## Working with the plugin

The setup is fairly simple - you only need to do the following two things:

### Add a ``Plugin`` class
Create a plugin class in your bundle. The best practice is to create a
standalone `Plugin` class in a `ContaoManager` folder/subnamespace. The
result would be a class like `Vendor\ContaoSomething\ContaoManager\Plugin`:

```php
 namespace Vendor\ContaoSomething\ContaoManager;
         
 class Plugin
 {    
 }       
```

This class can then implement any of the available interfaces to
work with the Contao Managed Edition (see below).

### Adjust your ``composer.json``

Each Composer package can have one plugin, and it must be registered
in the ``composer.json``.

1. Add a node `contao-manager-plugin` in the [`extra` section][composer-extra].
   The result will look something like this:

    ```json
    {
       "extra": {
            "contao-manager-plugin": "Vendor\\ContaoSomething\\ContaoManager\\Plugin"
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


## The interfaces
The following list gives an overview of the available interfaces/configurations.

> #### info:: Hint
> More interfaces will likely be added in the future when new features are
> added to Contao or the Contao Manager.


### BundlePluginInterface

The `Contao\ManagerBundle\ContaoManager\Bundle\BundlePluginInterface`
allows a plugin to load bundles into the Symfony kernel at boot time.

This method is usually implemented by a Composer package to load its
Symfony bundle and dependencies. If you're adding features to Contao, 
it's likely that you'll need to load your bundle at runtime with this
functionality. 

→  [Autoloading Contao 4 / Symfony bundles](bundle-autoloading.md)


### ConfigPluginInterface

The `Contao\ManagerBundle\ContaoManager\Config\ConfigPluginInterface` allows
a plugin to register container configuration at build time. This is similar
to prepending configuration in Symfony, but it is only executed
in a Contao *Managed Edition* application.

→  [Container configuration](container-configuration.md)


### RoutingPluginInterface

The `Contao\ManagerBundle\ContaoManager\Routing\RoutingPluginInterface`
enables a plugin to register custom routes for the Symfony router.

→  [Adding routes](routing.md)


### DependentPluginInterface

Some features, like prepending routing configuration, require a specific order
of plugins to correctly override each other. If your plugins needs to override
a route of another plugin, it must be loaded before that.

The `Contao\ManagerBundle\ContaoManager\Dependency\DependentPluginInterface`
allows to define a list of **Composer packages** whose plugins must be loaded
before the current plugin.

→  [Defining plugin dependencies](plugin-dependencies.md)



[composer-extra]: https://getcomposer.org/doc/04-schema.md#extra