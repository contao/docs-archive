# Setting up a local dev environment

Imagine you are developing a new bundle that has not been published yet. How do
you get that running in your current web project? There are lot's of different
ways to achieve this but most of them require you to update your project via 
``composer update`` on every code change, which is way too cumbersome. Here is
an alternative way to do it:

## Composer and local repositories 

Assume your Contao web project is called ``web1`` and your new bundle
``my-name/contao-something``. Your bundle can be developed outside your web
project's directory. In this example ``../_bundles/contao-something`` would be
the relative path seen from the web project root.
   
    <webdev>
     ├─ _bundles
     │   └─ contao-something
     │       ├─ composer.json
     │       └─ ...
     ├─ web1
     │   ├─ composer.json
     │   └─ ...
     └─ web2
         └─ ...


After your new bundle contains at least it's ``composer.json`` you can add it
as a new requirement to your web project like you would with every other
resource. Here comes the important part: You need to add a new key called 
``repositories`` to your web project's ``composer.json``, in which you define
the relative or absolute ``path`` to your bundle. If you do so, composer will 
create a symlink to the package in the web project's vendor directory instead
of copying the sources. So now the files being load from your application are
the same files you are editing.
   
Here is how this setting looks like (excerpt from the ``composer.json``):

```json
{
  "name": "contao/managed-edition",
  "require": {
    //...
    
    "my-name/contao-something": "dev-master"
  },
  "repositories": [
    {
      "type": "path",
      "url": "../_bundles/contao-something"
    }
  ]
}
```

There is only a little caveat: Composer infers the bundle's version from the
git tags. If you haven't versioned and tagged your bundle yet or do not plan to
do so, to the version defaults to ``dev-master``. If you did not configure a
higher minimal stability, the default settings would therefore not allow
installing it. You can circumvent that by doing one of the following three
things:
- explicitly require ``dev-master`` (like in the example above) 
- version and tag your bundle with a ``stable`` version before installing
- raise your minimal stability to ``dev`` (probably not a good idea if not set already)


**Using your bundle in multiple projects**

It's a good idea to have the bundle's root outside your project directory. This
way it won't interfere with with versioning plus it gives you the opportunity
to use it in a second local project (say ``web2``) without coupling them.
   
When you are ready to publish your web project (after having
[published your bundle](bundle-dev/publish.md)) make sure that you don't add
the repositories key to your remote ``composer.json``. If you registered your
bundle on *Packagist* there is nothing more to do. It's a good idea to leave
the key in your local/dev environment for further development though. 


## Working in the ``vendor`` folder: *prefer sources* 

Here is another one: If you do not need more than one project to include your
bundle during development and if your bundle already got installed via composer
you can simply develop in the ``vendor`` folder itself. This is especially
useful if you for instance want to write a pull request for an official Contao
bundle.

To make this work manually *delete* the bundle's folder after installing it and
let composer update the package again but now with the ``prefer-source`` option
set:

> composer update my-name/contao-something --prefer-source

This will make the package available with source control information (``.git``)
and allows you to commit and push directly directly from inside the ``vendor``
folder. In some rare cases where part of your code relies on living in exactly
this path (relative to the project root), this might be the only way to achieve
it.  


## Caching hurdles ##

Caching is very powerful in production, in development it can make things quite
inconvenient. As a side note here are some shortcuts good to know:

* Use the ``app_dev.php`` entry point. Not only does it provide useful
  information in the debugger toolbar or when exceptions occur, it also has
  caching deactivated for most parts by default. If you just added a new
  backend module that does not appear or you are clearing the cache every time
  you are tweaking a dca field, try this one instead.

* Run ``composer dump-autoload`` to regenerate the autoload files. If you are
  using a PSR-4 class root in your bundle and you are not using autoloader
  optimizations (which is recommended during development for exactly these
  reasons) you'll only have to run this if your class root changes. If you use
  class maps in your bundle, however, for these you must call it whenever you
  add a new one.