# Bundle development - getting started

Start writing your first bundle today. The abundance of possibilities that come
with Symfony might look overwhelming at first but it's really not that hard.

> "A bundle is similar to a plugin in other software, but even better."  
> -- Symfony Docs 

So what are you waiting for? :-) 


## What do I need to know?
In short: If you're able to write a Symfony bundle, you are also able to write
an extension for Contao 4 as this is the *same thing* right now. Contao 4 itself
consists of several bundles (Core, News, Faq, Comments, Calendar, …) and yours
could be yet another one that adds the functionality you need.

As a Contao 3 developer, start here:

 1) Get familiar with Symfony and the concepts of a bundle. Luckily this is
    [very well documented][SymfonyBundles] and not much more than a folder
    structure, a bundle class and a Composer definition. 
 
 2) Get familiar with [Composer][ComposerIntro] as this is the default way in
    Symfony to install bundles and manager their dependencies.
    
 
## Quick start for Contao 3 developers

Do you need some examples? It's a good idea trying to understand how the 
implementation of the Contao default bundles works. To begin with have a look
at the smaller ones like the [NewsBundle][NewsBundle] (rather than the core). 

Here are some things to help you get oriented:

 - Namespaces follow [PSR-4][PSR-4] recommendations with the folder ``src``
   typically defined to be the namespace root.
   
 - The ``composer.json`` contains meta data and defines the bundle's
   requirements (a bit like the ``autoload.ini`` in Contao 3 but way more
   powerful).
   
 - The folder ``src/Resources`` contains all the (typically) non-code things
   that are considered a *resource*. Like: configuration, templates, images, …
   
 - Things known from Contao 3 that are still present (e.g. ``dca`` definitions,
   a module's ``config.php``, language files, …) now live under
   ``src/Resources/contao``.
   
 - ``src/ManagerPlugin`` contains the [bits](../managed-edition/plugins.md)
   that enable the bundle to run inside a *Contao Managed Edition*.
 

> #### warning:: Warning
> Note that the Contao Core itself is in the process of migrating to Symfony.
> So most of the code found under ``core-bundle/src/Resources/contao/``
> is legacy and should not be considered in terms of bundle best practice.    


## Cookbook 
Also you might want to take a look at the quick start section in the
*Contao Cookbook*. 

> TODO: add reference  



[SymfonyBundles]: https://symfony.com/doc/current/bundles.html
[ComposerIntro]: https://getcomposer.org/doc/00-intro.md
[NewsBundle]: https://github.com/contao/news-bundle
[PSR-4]: http://www.php-fig.org/psr/psr-4/