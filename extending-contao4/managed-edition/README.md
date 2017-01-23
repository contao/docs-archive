# Contao 4 – Managed Edition

Starting with version 4.3.4, Contao is available as a so-called
*Managed Edition*. Compared to a regular Symfony application, a 
*Managed Edition* is limited in its customization possibilities to 
allow automatic management by third-party bundles.


## Differences to Contao Standard Edition


### AppKernel

Contao *Managed Edition* does not feature an `AppKernel` class that can be
customized. Bundles are automatically loaded by *Plugins* so users do not need
to know how to write PHP code or what classes to instantiate in what order.


### Config files

In a Contao *Managed Edition*, the configuration is loaded by plugins
and not by application configuration files. This will allow the
application to work without manually adjusting files.


### Console

A Symfony application usually contains a console script in `bin/console`.
In Contao *Managed Edition* the console is part of the
`contao/manager-bundle` and installed in `vendor/bin/contao-console`.

> #### info:: Hint
> If you are an experienced Symfony developer and missing the default
> location of the console at `bin/console`, just add a symlink for
> your convenience: `ln -s ./../vendor/bin/console ./bin/console`.

### Autoloading Contao 3 extensions

Similar to the behavior in Contao 3, the Contao 4 *Managed Edition*
will automatically load all extensions in `system/modules`. The
implementation is designed to work as in Contao 3, so the `autoload.ini`
is taken into account, and an extension can be disabled by placing a
`.skip` file into the extension folder.


## Customizing the application

The Contao *Managed Edition* is not a standard Symfony application,
so you can't simply edit the config files. In addition to loading 
configuration from packages installed by Composer, you can customize
an installation in several ways.


### Adding a config file

There are two configuration files available in Contao *Managed Edition*:

1. `app/config/parameters.yml` contains parameters like database
    credentials. The file is created and updated by the install tool.

2. `app/config/config.yml` can be created manually to adjust the
    Symfony configuration. This config file is loaded after all plugins.


### Adding resources

The `app/Resources` directory behaves exactly like in a Symfony standard
application, meaning you can override Twig templates etc. If you want
to override Contao resources like DCA files, you can simply add them
to `app/Resources/contao` and they will be loaded at runtime.


### Adding an AppBundle

As [recommended by Symfony][AppBundle], the AppBundle should be your main 
bundle if you need to customize the application. Fortunately, the
AppBundle is automatically loaded in Contao *Managed Edition* if the
class can be found.


### Adding a Manager Plugin

Each application can have one global class `ContaoManagerPlugin` which
will be automatically loaded if it exists. We recommend this to be
located in your `app` folder, but that does not really matter as long
as the Composer class loader can find it.

Using a custom plugin you can adjust all features of the application
in the same way any Composer package can do. The `ContaoManagerPlugin`
will be loaded last, so you can always override any existing setup.



[AppBundle]: http://symfony.com/doc/current/best_practices/business-logic.html
