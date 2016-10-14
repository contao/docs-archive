## Extensions and bundles

Extensions are an essential part of Contao, because they allow you to add extra
functionality. There are more than 1,800 extensions available in the Contao
[Extension Repository][1].

Contao 4 is built on top of the Symfony framework and takes advantage of its
functionalities but also of its terminology. In a Symfony project, an extension
is named a bundle.


### Finding extensions or bundles

Contao has its own [repository][1] where you can find the extensions that are
compatible with Contao 3.x and lower.

The second most commonly used repository is [Packagist][2]. It lists the
extensions and bundles installable through [Composer][3].
 
1. [List of Contao 4 bundles][4] in Packagist.
2. [List of Contao 3 extensions][5] in Packagist.


### Installing a bundle with Composer

A name of a bundle is divided into two parts. The first part is the name of the
vendor (project owner) and the second the bundle name. For example:
`contao/news-bundle`.

Run the command `composer require vendor/bundleName` in your
command-line interface to start the installation.

Contao dependencies (in our case a bundle) are described in a file named
`composer.json` which is located in the root folder of your Contao installation.
During the installation process, Composer updates the `composer.json` file and
determines itself which version of the bundle is best suited to be installed
depending on your version of Contao.

Then you must register your bundle in `app/AppKernel.php` so that it can be
taken into account by the system. Add the bundle to the list of registered
bundles:

```php
<?php
// app/AppKernel.php

// ...
class AppKernel extends Kernel
{
    public function registerBundles()
    {
        $bundles = [
            // ...

            new <vendor>\<bundle-name>\<bundle-long-name>(),
        ];

        // ...
    }

    // ...
}
```

Finally, check the database with the [Contao install tool][7].

With Composer, the cache is cleared automatically.


### Installing a Contao extension

An extension can be installed with Composer or manually. With Composer, the
installation process is the same as a bundle except for the registration in the
`app/AppKernel.php` file where the code is slightly different.

In the example below, the first parameter `myExtensionName` should be replaced
by the name of your extension:

```php
<?php
// app/AppKernel.php

// ...
class AppKernel extends Kernel
{
    public function registerBundles()
    {
        $bundles = [
            // ...

            new Contao\CoreBundle\HttpKernel\Bundle\ContaoModuleBundle('myExtensionName', $this->getRootDir()),
        ];

        // ...
    }

    // ...
}
```


#### Manually

Almost all extensions for Contao 3 are also compatible with Contao 4. If a
Contao 3 extension is not available on Composer, you can install it manually
and try if it works with Contao 4. Be aware that you must also take care of
installing all dependencies as listed in the Extension Repository.

Find the extension you want to install in the [Extension Repository][1] and
download the .zip archive of the latest release. Then unzip the files and copy
them to the `system/modules` folder. If the extension has public files, you must
generate a [symbolic link][6] with the command `php app/console contao:symlinks`
in your command-line interface.

Then you must register your extension in `app/AppKernel.php` so that it can be
taken into account by the system (see the previous chapter). Finally, check the
database with the [Contao install tool][7].

When you have made all the installation procedure, you can clear the cache with
the following command: `php app/console cache:clear -e=prod`.


## Extension catalog

Prior to Contao 4, it was possible to install an extension automatically from
the back end. This feature is under development and will be offered in a future
release.


[1]: https://contao.org/en/extension-list.html
[2]: https://packagist.org
[3]: https://getcomposer.org/doc/00-intro.md#introduction
[4]: https://packagist.org/search/?q=&type=contao-bundle
[5]: https://packagist.org/search/?q=&type=contao-module
[6]: https://docs.contao.org/books/cookbook/en/folder-structure.html#symbolic-link
[7]: ../01-installation/installing-contao.md#the-contao-install-tool
