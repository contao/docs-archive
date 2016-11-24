# Contao 4 – Managed Edition

Starting with version 4.3, Contao is available as a so-called *Managed Edition*.
Compared to a regular Symfony application, a *Managed Edition* is limited
in its customization possibilities to allow automatic management by 
third-party bundles.


## Differences to Contao Standard Edition


### AppKernel

Contao *Managed Edition* does not feature an `AppKernel` class that can be
customized. Bundles are automatically loaded by *Plugins* so users do not need
to know how to write PHP code or what classes to instantiate in what order.


### Config files

Contao *Managed Edition* does not feature the regular Symfony config files
in `app/config`. Instead, all configurations are loaded by bundles using the
Symfony *[Prepend configuration]* interface.


## Customizing the application

The Contao *Managed Edition* is not a standard Symfony application,
so you can't simply edit the config files. In addition to loading 
configuration from packages installed by Composer, you can customize
an installation in several ways.


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



[Prepend configuration]: http://symfony.com/doc/current/bundles/prepend_extension.html
[AppBundle]: http://symfony.com/doc/current/best_practices/business-logic.html
