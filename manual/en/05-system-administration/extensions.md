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

With Contao 4.0, the installation must be performed manually as described below:

Find the extension you want to install in the [extension list][1] and download
the .zip archive of the latest release. Then unzip the files and copy them to
the `system/modules` folder. If the extension has public files, you must
generate a [symbolic link][2] with the command `app/console contao:symlinks` in your
command-line interface. Then you must register your extension in
`app/AppKernel.php` so that it can be taken into account by the system (see
below). Finally, check the database with the [Contao install tool][3].


#### AppKernel.php

1. Add the `use` statement.

```php
use Contao\CoreBundle\HttpKernel\Bundle\ContaoModuleBundle;
```

2. Instantiate the `ContaoModuleBundle` class. The first parameter is the name
of your extension.

```php
new ContaoModuleBundle('myExtensionName', $this->getRootDir()),
```

**Example**:

```php
// app/AppKernel.php
use Contao\CoreBundle\HttpKernel\Bundle\ContaoModuleBundle;

public function registerBundles()
{
    $bundles = [
        new Symfony\Bundle\FrameworkBundle\FrameworkBundle(),
        new Contao\CoreBundle\ContaoCoreBundle(),
        new ContaoModuleBundle('myExtensionName', $this->getRootDir()),
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
[2]: ../02-folder-structure/README.md#symbolic-link
[3]: ../01-installation/installing-contao.md#the-contao-install-tool
