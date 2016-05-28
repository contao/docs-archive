## Extensions

Extensions are an essential part of Contao, because they allow you to add extra
functionality. There are more than 1,800 extensions available in the Contao
[Extension Repository][1].

Contao 4 is built on top of the Symfony framework and takes advantage of its
functionalities but also of its terminology. In a Symfony project, an extension
is named a bundle.

If a bundle and a Contao extension have the same purpose, they are nevertheless
not developed in the same way and the installation procedure is different for
each of them.

> **Warning** Even if a Contao extension can be installed, this does not mean
that it is compatible with Contao 4. The extension you want to use must take
into account the prerequisites of the version 4.


### Installing a Contao extension

With Contao 4.0, an extension can be installed with [Composer][2] or manually.


#### With Composer

An extension that can be installed via Composer can be found through its main
repository [Packagist][3]. A name of an extension is divided into two parts.
The first part is the name of the vendor (project owner) and the second the
extension name. For example: `vendor/extensionName`.

Dependencies (in our case an extension) are described in a file named
`composer.json` which is located in the root folder of your Contao installation.

Run the command `php composer.phar require vendor/extensionName` in your
command-line interface to start the installation.

Composer updates the `composer.json` file and determines itself which version
of the extension is best suited to be installed depending on your version of
Contao.

Then you must register your extension in `app/AppKernel.php` so that it can be
taken into account by the system (see "Enable the extension" chapter below).
Finally, check the database with the [Contao install tool][5].

With Composer, the cache is cleared automatically.


#### Manually

Find the extension you want to install in the [Extension Repository][1] and
download the .zip archive of the latest release. Then unzip the files and copy
them to the `system/modules` folder. If the extension has public files, you must
generate a [symbolic link][4] with the command `app/console contao:symlinks` in
your command-line interface.

Then you must register your extension in `app/AppKernel.php` so that it can be
taken into account by the system (see "Enable the extension" chapter below).
Finally, check the database with the [Contao install tool][5].

When you have made all the installation procedure, you can clear the cache with
the following command: `php app/console cache:clear -e=prod`.


#### Enable the extension

You need to enable your extension by adding it to the list of registered
bundles in the `app/AppKernel.php` file of your Contao folder.

Add the following line as in the example below by changing the first parameter
`myExtensionName` with the name of your extension.

```php
new Contao\CoreBundle\HttpKernel\Bundle\ContaoModuleBundle('myExtensionName', $this->getRootDir()),
```

**Example**:

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


## Extension catalog

Prior to Contao 4, it was possible to install an extension automatically from
the back end. This feature is under development and will be offered in a future
release.


[1]: https://contao.org/en/extension-list.html
[2]: https://getcomposer.org/doc/00-intro.md#introduction
[3]: https://packagist.org
[4]: ../01-installation/installing-contao.md#symbolic-link
[5]: ../01-installation/installing-contao.md#the-contao-install-tool
