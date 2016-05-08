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

With Contao 4.0, an extension can be installed with Composer or manually.


#### With Composer

An extension that can be installed via Composer can be found through its main
repository [Packagist][2]. A name of an extension is divided into two parts.
The first part is the name of the project owner and the second the extension
name. For example: `companyName/extensionName`.

Dependencies (in our case an extension) are described in a file named
`composer.json` which is located in the root folder of your Contao installation.

This is the first step you need to do. Open the `composer.json` file and add the
new dependency in the `require` key.

```json
"require": {
        "companyName/extensionName": "~1.0",
    },
```

You must also enter the version you want to use. The `~` [operator][3] means you
want the latest version of `1.*`.

Run the command `php composer.phar update companyName/extensionName` in your
command-line interface to start the installation.


#### Manually

Find the extension you want to install in the [Extension Repository][1] and
download the .zip archive of the latest release. Then unzip the files and copy
them to the `system/modules` folder. If the extension has public files, you must
generate a [symbolic link][4] with the command `app/console contao:symlinks` in
your command-line interface. Then you must register your extension in
`app/AppKernel.php` so that it can be taken into account by the system (see
below). Finally, check the database with the [Contao install tool][5].


##### AppKernel.php

Instantiate the `ContaoModuleBundle` class. The first parameter is the name of
your extension.

```php
new Contao\CoreBundle\HttpKernel\Bundle\ContaoModuleBundle('myExtensionName', $this->getRootDir()),
```

**Example**:

```php
// app/AppKernel.php

public function registerBundles()
{
    $bundles = [
        new Symfony\Bundle\FrameworkBundle\FrameworkBundle(),
        new Contao\CoreBundle\ContaoCoreBundle(),
        new Contao\CoreBundle\HttpKernel\Bundle\ContaoModuleBundle('myExtensionName', $this->getRootDir()),
    ];

    // ...

    return $bundles;
}
```


## Extension catalog

Prior to Contao 4, it was possible to install an extension automatically from
the back end. This feature is under development and will be offered in a future
release.


[1]: https://contao.org/en/extension-list.html
[2]: https://packagist.org
[3]: https://getcomposer.org/doc/articles/versions.md#tilde
[4]: ../01-installation/installing-contao.md#symbolic-link
[5]: ../01-installation/installing-contao.md#the-contao-install-tool
