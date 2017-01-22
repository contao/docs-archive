## Extensions et bundles

Les extensions sont une partie essentielle de Contao, car ils vous permettent
d'ajouter des fonctionnalités supplémentaires. Contao 4 est basé sur le
framework Symfony et tire profit de ses fonctionnalités et de sa terminologie.
Dans Contao 4, Vous pouvez utiliser des extensions des précédentes versions de
Contao ainsi que les bundles.


### Trouver des extensions ou des bundles

Contao a son propre [référentiel][1] où vous pouvez trouver les extensions qui
sont compatibles avec Contao 3.x et antérieures.

Le second référentiel le plus couramment utilisé est [Packagist][2]. Il liste
les extensions et bundles qui peuvent être installés par [Composer][3].

1. [Liste des bundles de Contao 4][4] dans Packagist.
2. [Liste des extensions de Contao 3][5] dans Packagist.


### Installer un bundle avec Composer

Le nom d'un bundle est divisé en deux parties. La première partie est le nom du
"vendor" (propriétaire du projet) et le second, le nom du bundle. Par exemple :
`contao/news-bundle`.

Exécutez la commande `composer require vendor/bundleName` dans votre interface
en ligne de commande afin de démarrer l'installation.

Les dépendances de Contao (dans notre cas un bundle) sont décrites dans un
fichier nommé `composer.json` qui est situé dans le dossier racine de votre
installation de Contao. Au cours du processus d'installation, Composer met à
jour le fichier `composer.json` et détermine lui-même quelle version du bundle
est la mieux adaptée pour être installée en fonction de votre version de Contao.

Ensuite, vous devez enregistrer votre bundle dans `app/AppKernel.php` afin
qu'il puisse être pris en compte par le système. Ajoutez le bundle à la liste
des bundles enregistrés :

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

Enfin, vérifiez la base de données avec l'[outil d'installation de Contao][7].

Avec Composer, le cache est automatiquement effacé.


### Installer une extension de Contao

Une extension peut être installée avec Composer ou manuellement. Avec Composer,
le processus d'installation est le même que celui d'un bundle à l'exception de
l'enregistrement dans le fichier `app/AppKernel.php` où le code est légèrement
différent.

Dans l'exemple ci-dessous, le premier paramètre `myExtensionName` doit être
remplacé par le nom de votre extension :

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


#### Manuellement

Presque toutes les extensions pour Contao 3 sont également compatibles avec
Contao 4. Si une extension de Contao 3 n'est pas disponible avec Composer, vous
pouvez l'installer manuellement et essayer s'il fonctionne avec Contao 4. Soyez
conscient que vous devez aussi prendre soin d'installer toutes les dépendances
comme indiqué dans le référentiel d'extensions.

Trouver l'extension que vous souhaitez installer dans le
[référentiel d'extensions][1] et télécharger l'archive .zip de la dernière
version. Puis, décompressez les fichiers et copiez-les dans le dossier
`system/modules`. Si l'extension a des fichiers publics, vous devez générer un
[lien symbolique][6] avec la commande `php app/console contao:symlinks` dans
votre interface en ligne de commande.

Ensuite, vous devez enregistrer votre extension dans `app/AppKernel.php` afin
qu'elle puisse être prise en compte par le système (voir le chapitre précédent).
Enfin, vérifiez la base de données avec l'[outil d'installation de Contao][7].

Lorsque vous avez effectué toute la procédure d'installation, vous pouvez
effacer le cache avec la commande suivante :
`php app/console cache:clear -e=prod`.


## Catalogue d'extensions

Avant Contao 4, il était possible d'installer automatiquement une extension à
partir du back office. Cette fonctionnalité est en cours de développement et
sera proposée dans une version ultérieure.


[1]: https://contao.org/en/extension-list.html
[2]: https://packagist.org
[3]: https://getcomposer.org/doc/00-intro.md#introduction
[4]: https://packagist.org/search/?q=&type=contao-bundle
[5]: https://packagist.org/search/?q=&type=contao-module
[6]: https://fr.wikipedia.org/wiki/Lien_symbolique
[7]: ../01-installation/installer-contao.md#loutil-dinstallation-de-contao
