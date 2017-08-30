# Contao 4 – Managed Edition


Starting with version 4.3.4, Contao is available as a so-called
*Managed Edition*. Compared to a regular Symfony application, a 
*Managed Edition* is limited in its customization possibilities to 
allow automatic management by third-party bundles.


## Background

A regular Symfony application consists of a collection of bundles (typically
installed via composer), some configuration and application specific code.
Typically there is a class called ``AppKernel.php`` where the bundles which
should get loaded can be registered.

So installing/removing a new bundle typically means
 1. updating the composer requirements - installing/removing the component
 2. adjusting the configuration (e.g. routes, parameters)
 3. adding/removing a line of code to ``AppKernel.php`` (registering the bundle)
  
These are rather technical tasks that involve editing code files and using the
command line which would normally prevent non-technical users from updating the
software or adding/removing extensions. 

Contao 4 therefore comes prepacked in two versions: The *Standard* and the
*Managed Edition*. While the *Standard Edition* behaves just like a regular
Symfony application, the *Managed Edition* (together with the 
[Contao Manager][ContaoManager]) tries to automate all of the needed
adjustments.
 
**Things work slightly different in the *Managed Edition*…**
 
The *Managed Edition* comes with the trade-off that some customizations
might be harder to achieve than with a default Symfony application and it means
that it shifts the rather complex tasks (like registering configuration,
loading order or routes etc.) to the developers rather than the users. This is
why writing a manager plugin *might* seem complicated at first sight. But hey,
someone's got to do the work. ;-)

(Furthermore as no ``AppKernel.php`` exists in the managed edition
there are custom mechanisms e.g. to load an ``AppBundle`` or setup custom
routes - have a look into the Contao 4 Cookbook to find out more about this.)    


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
The *Contao Managed Edition* is not a standard Symfony application,
so you cannot simply edit the config files. In addition to loading 
configuration from packages installed by Composer, you can customize
an installation in several ways.

→ [Customizing the Managed Edition](customizing.md)  



[ContaoManager]: https://github.com/contao/contao-manager