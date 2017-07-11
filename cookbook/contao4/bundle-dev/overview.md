# Overview and basic structure

Writing a Contao 4 bundle is not hard. If you have experience developing Contao 3 extensions you'll only have to
understand the basic structure of a Symfony bundle ([which is documented very well](https://symfony.com/doc/bundles/)) 
to get started. This guide focuses on some aspects that are special to Contao.   


## Standard vs. Managed edition

A regular Symfony application consists of a collection of packages/bundles (typically installed via composer), some
configuration and application specific code. Typically there is a class called ``AppKernel.php`` in which the bundles
that shall get loaded are registered. So installing a new feature typically means
 1. updating the composer requirements / installing the component
 2. adjusting the configuration (e.g. routes, parameters)
 3. adding a new line of code to ``AppKernel.php`` (registering the bundle)
  
Contao 4 (which basically is a collection of symfony bundles + configuration) comes prepacked in two versions: The
*standard* and the *managed edition*. The *standard edition* behaves like a typical Symfony application (see above), the
*managed edition* (together with the [Contao Manager](https://github.com/contao/contao-manager)) tries to ease the
process to be less technical so that there is no configuring and manually registering necessary. (The trade-off of this
version is that some special customizations might be harder to achieve than with a default symfony application.)

**Things work slightly different in the managed edition…**

This however means that a bundle that works in the managed edition will have to ship a basic configuration and tell the
system somehow how it should be loaded. (Furthermore as no ``AppKernel.php`` exists in the managed edition there are
custom mechanisms e.g. to load an ``AppBundle`` or setup custom routes. But this belongs to another section.)    


## Basic structure

The Symfony docs already define some [best practices](https://symfony.com/doc/current/bundles/best_practices.html) which
are worth reading. Here is how your ``my-name/contao-something`` bundle could be structured in a bit more detail:

    <contao-something>
      ├─ src
      │   ├─ DependencyInjection
      │   │   ├─ Configuration.php
      │   │   └─ MyNameContaoSomethingExtension.php
      │   ├─ Resources
      │   │   ├─ config
      │   │   │   ├─ routing.yml
      │   │   │   └─ services.yml
      │   │   ├─ contao            
      │   │   │   ├─ config                                    
      │   │   │   │   └─ config.php                                    
      │   │   │   ├─ dca            
      │   │   │   │   ├─ tl_content.php                                    
      │   │   │   │   └─ tl_myname_fancy_thing.php                                    
      │   │   │   ├─ languages
      │   │   │   │   └─ ...                                    
      │   │   │   └─ templates         
      │   │   │       └─ ...                                    
      │   │   └─ public            
      │   │       └─ css                                    
      │   │           └─ ...         
      │   ├─ Modules
      │   │    └─ FancyThingModule.php         
      │   ├─ ContaoManagerPlugin.php
      │   └─ MyNameContaoSomethingBundle.php
      ├─ tests
      │   └─ ...
      ├─ composer.json
      ├─ LICENSE
      └─ README.md

Note that the files inside the directory structure follow PSR-4 namespace rules. So if ``src`` is your namespace root
(``MyName/ContaoSomething``), the content of the file ``src/Modules/FancyThingModule.php`` should live inside the
``MyName/ContaoSomething/Modules`` namespace.   

There are some typical directories: 
* The directory ``src/Resources/contao`` holds the 'old' things known from Contao 3 extensions like dca definitions, 
contao config, language files (no ``autoload.php`` or ``autoload.ini`` however as this is not needed anymore).
* The directory ``src/Resources/config`` contains optional symfony config files (e.g. routing, services).
* Inside the ``src/DependencyInjection`` directory the extension's [configuration]((bundle-dev/configuration.md)) gets
set up if any.
 
As well as some special files:
* ``src/MyNameContaoSomethingBundle.php`` identifies the directory as a bundle (see Symfony docs - basically it's 
  nothing more than a class extending ``Symfony\Component\HttpKernel\Bundle\Bundle``).
* ``src/ContaoManagerPlugin.php`` contains the magic that makes this bundle work in the managed edition.

The ``composer.json`` for this bundle contains meta data, requirements / dependencies to other packages, and defines 
how it is structured / should be loaded. The file could look like this (for clarity fields like author, description, … 
are let out):

```json
{
  "name": "my-name/contao-something",
  "type": "contao-bundle",
    "require": {
    "php": ">=7.1",
    "contao/core-bundle": "^4.4.0"
  },
  "require-dev": {
    "contao/manager-plugin": "^2.0"
  },
  "autoload": {
    "psr-4": {
      "MyName\\ContaoSomething\\": "src/"
    }
  },
  "extra": {
    "contao-manager-plugin": "MyName\\ContaoSomething\\ContaoManagerPlugin"
  }
}
```

Note how autoloading is configured to use ``src`` as the PSR-4 root. The ``ContaoManagerPlugin.php`` gets specified in
the ``extra`` section. See the [composer docs](https://getcomposer.org/doc/01-basic-usage.md) to find out more about the
format of this file.