> TODO: rewrite

# Overview and basic structure

Writing a reusable Contao 4 bundle is not hard. If you have experience developing
Contao 3 extensions you'll quickly find your way.

Before we start, check out these overview sections from the Contao 4 developer
reference:  
→ [Overview][extC4-Overview]  
→ [Getting started][extC4-GettingStarted]  

> #### warning:: Note
> At this point you should be sure that you do *not* want to write an
> ``AppBundle`` but a reusable one. Many things hold true for an ``AppBundle``
> as well, but these things won't get pointed out in this documentation.  

## Basic structure

Let's start by creating the basic directory structure.

The Symfony docs already define some [best practices][SymfonyBestPractices]
which are worth reading. Here is how your ``my-name/contao-something`` bundle
could be structured in a bit more detail:

    <contao-something>
      ├─ src
      │   ├─ ContaoManager
      │   │    └─ Plugin.php      
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
      │   └─ MyNameContaoSomethingBundle.php
      ├─ tests
      │   └─ ...
      ├─ composer.json
      ├─ LICENSE
      └─ README.md

Note that the files inside the directory structure follow PSR-4 namespace
rules. So if ``src`` is your namespace root (``MyName/ContaoSomething``), the
content of the file ``src/Modules/FancyThingModule.php`` should live inside
the ``MyName/ContaoSomething/Modules`` namespace.

There are some typical directories: 
* The directory ``src/Resources/contao`` holds the 'old' things known from
  Contao 3 extensions like dca definitions, contao config, language files
  (no ``autoload.php`` or ``autoload.ini`` however as this is not needed
  anymore).  
* The directory ``src/Resources/config`` contains optional symfony config
  files (e.g. routing, services).
* Inside the ``src/DependencyInjection`` directory the extension's
  [configuration]((bundle-dev/configuration.md)) gets set up if any.
 
 
As well as some special files:
* ``src/MyNameContaoSomethingBundle.php`` identifies the directory as a bundle
   (see Symfony docs - basically it's  nothing more than a class extending 
   ``Symfony\Component\HttpKernel\Bundle\Bundle``).  
* ``src/ContaoManager/Plugin.php`` contains the magic that makes this bundle
   work in the managed edition.

The ``composer.json`` for this bundle contains meta data, requirements / 
dependencies to other packages, and defines how it is structured / should be
loaded. The file could look like this (for clarity fields like author,
description, … are let out):

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
    "contao-manager-plugin": "MyName\\ContaoSomething\\ContaoManager\\Plugin"
  }
}
```

Note how autoloading is configured to use ``src`` as the PSR-4 root. The 
Manager Plugin (``Plugin.php``) gets specified in the ``extra`` section. See
the [composer docs][ComposerBasicUsage] to find out more about the format of
this file.



[extC4-Overview]: ../../../extending-contao4/bundle-dev/README.md
[extC4-GettingStarted]: ../../../extending-contao4/bundle-dev/getting-started.md
[SymfonyBestPractices]: https://symfony.com/doc/current/bundles/best_practices.html
[ComposerBasicUsage]: https://getcomposer.org/doc/01-basic-usage.md