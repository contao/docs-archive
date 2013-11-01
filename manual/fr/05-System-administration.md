# Administration du système

Les chapitres suivants expliquent comment administrer Contao. Outre l'installation et la mise à jour de l'application, un administrateur est responsable de la création des utilisateurs et des groupes d'utilisateurs, gérer les modules additionnels et la maintenance du système.


## Utilisateurs et groupes d'utilisateurs

Contao fait une distinction entre les utilisateurs du back office ("utilisateurs"), qui peuvent se connecter au panneau d'administration, et les utilisateurs front office («membres»), qui peuvent se connecter au site internet. Contrairement aux administrateurs, qui ont accès à toutes les pages et à tous les éléments par défaut ("allow all"), les utilisateurs ne peuvent pas accéder à une ressource qui n'a pas été explicitement autorisée dans leur profil ou dans le profil de l'un des groupes d'utilisateurs auxquels ils appartiennent ("deny all").


### Utilisateurs

Chaque utilisateur peut être associé à plusieurs groupes d'utilisateurs et hérite automatiquement de leurs autorisations. Toutes les autorisations sont cumulatives, ce qui signifie que l'utilisateur hérite de la somme des permissions de tous les groupes auxquels il appartient. Si le groupe A accorde un certain droit, vous ne pouvez pas la révoquer dans le groupe B.


#### Pages autorisées

L'option "Pages autorisées" permet de définir quelles pages de la structure du site, l'utilisateur est autorisé à voir. La capture d'écran ci-dessous montre la structure du site telle qu'elle est perçue par Helen Lewis. Bien que le site internet contient beaucoup plus de pages, elle ne peut en voir que trois, parce que seul l'accès à la page "Courses" a été autorisé dans les paramètres du groupe "Editors". Notez que même si Helen Lewis est autorisée à voir trois pages, elle ne peut modifier que l'une d'elles !

![](https://raw.github.com/contao/docs/3.1/manual/en/images/site-structure-hlewis.jpg)

Être capable de voir une page n'inclut pas le droit de la modifier (ou de modifier ses articles). Rappelez-vous que [les permissions d'une page][1] sont définies dans la structure du site, donc pour permettre l'accès à une page à un utilisateur, vous devez le sélectionner dans son profil et accorder son accès dans la structure du site.


#### Répertoires autorisés

Semblable à l'option "Pages autorisées", l'option "Répertoires autorisés" défini quels répertoires un utilisateur est autorisé à voir. Ci-dessous, une capture d'écran du gestionnaire de fichiers tel qu'il est perçu par Helen Lewis. Elle n'est autorisée que de voir le répertoire "campus", alors que les administrateurs peuvent voir le répertoire complet des fichiers (`files`).

![](https://raw.github.com/contao/docs/3.1/manual/en/images/file-manager-hlewis.jpg)


#### Champs autorisés

Comme mentionné au début, les utilisateurs n'ont pas du tout de permissions par défaut ("deny all"), ce qui implique aussi qu'ils ne peuvent pas accéder aux champs d'un formulaire. Même s'ils sont par exemple autorisés à accéder au module d'actualités, le formulaire pour créer une nouvelle entrée sera vide jusqu'à ce que l'administrateur sélectionne un ou plusieurs champs de la table `tl_news` dans les paramètres du groupe.

![](https://raw.github.com/contao/docs/3.1/manual/en/images/allowed-fields.jpg)


### Membres

La gestion des membres (utilisateurs front office) est beaucoup plus facile que de gérer des utilisateurs back office, car il n'y a pas de pages ou de champs à autoriser. La gestion des membres est principalement requise pour contrôler l'accès aux pages protégées, qui est mis en œuvre au niveau du groupe. En fonction de la configuration du site internet, les membres inscrits pourront voir des pages protégées ou accéder à des téléchargements protégés qui ne sont pas disponibles pour les invités.


## Extensions

Les extensions sont une partie essentielle de Contao, car ils vous permettent d'ajouter des fonctionnalités supplémentaires. Il existe plus de 1400 extensions disponibles dans le référentiel d'extensions de Contao, que vous pouvez parcourir directement à partir du back office. La communication avec le serveur de référentiel s'effectue via SOAP, donc vous devez activer l'extension SOAP de PHP pour utiliser le service (si elle n'est pas activée par défaut).


### Catalogue d'extensions

Le module "Catalogue d'extensions" vous permet de parcourir la liste des extensions et d'installer des extensions par simple pression d'un bouton. Utilisez les options de filtrage et de tri pour trouver une extension particulière et cliquez sur l'icône d'information ou le titre de l'extension pour ouvrir la page de détails et installer le module.

![](https://raw.github.com/contao/docs/3.1/manual/en/images/extension-list.jpg)

La page de détails contient une description de l'extension et des informations importantes concernant les configurations du système requises, les versions et les dépendances d'autres modules. Cliquez sur le bouton "Installer" pour télécharger et installer l'extension.

![](https://raw.github.com/contao/docs/3.1/manual/en/images/extension-details.jpg)

Contao téléchargera et installera automatiquement l'extension et mettra à jour la base de données si nécessaire.

![](https://raw.github.com/contao/docs/3.1/manual/en/images/extension-install.jpg)


### Gestionnaire d'extensions

Le module "Gestionnaire d'extensions» vous permet de mettre à jour et de désinstaller les extensions. Il vérifie automatiquement les mises à jour et vous avertit si une nouvelle version est disponible. De nombreuses extensions incluent également des liens vers un manuel en ligne et/ou un fil de discussion dans un forum où vous pouvez obtenir de l'aide.

![](https://raw.github.com/contao/docs/3.1/manual/en/images/extension-manager.jpg)

Pour désinstaller une extension, cliquez simplement sur l'icône de désinstallation et suivez les instructions. Le gestionnaire d'extensions va supprimer tous les fichiers et répertoires et mettre à jour la base de données si nécessaire. Notez que cette action ne peut pas être annulée et les tables ne peuvent pas être restaurées !

![](https://raw.github.com/contao/docs/3.1/manual/en/images/extension-uninstall.jpg)


### Installation manuelle

Dans le cas où l'extension SOAP de PHP n'est pas disponible sur votre serveur, vous pouvez également installer des extensions de Contao manuellement. Trouvez le module correspondant dans la [liste des extensions][2] et téléchargez l'archive .zip de la dernière version. Ensuite, décompressez les fichiers et copiez-les dans votre répertoire local ou distant de Contao. Enfin, vérifiez la base de données avec l'[outil d'installation de Contao][3].


## Maintenance

Most of the maintenance jobs in Contao are executed automatically by the
Periodic Command Scheduler, so you can focus on your actual work. Even the tasks
in the maintenance module are carried out automatically, however sometimes it is
necessary to trigger them manually.


### Purger des données

Outre le contenu généré par l'utilisateur, Contao stocke beaucoup de données du système qui sont utilisées pour restaurer les enregistrements supprimés, revenir à des versions antérieures, créer l'index de recherche du site internet ou réduire le temps de chargement d'une page. Vous pouvez purger ces données manuellement par exemple pour supprimer les anciennes vignettes à partir du cache d'images ou pour recréer les fichiers XML du plan du site après que vous ayez modifié la structure du site.

![](https://raw.github.com/contao/docs/3.1/manual/en/images/purge-data.jpg)


### Reconstruire l'index de recherche

Les pages sont généralement ajoutées automatiquement à l'index de recherche quand ils sont vus dans le front office (sauf si vous êtes connecté au back office en même temps), donc vous n'avez donc pas besoin de vous inquiéter au sujet de l'index de recherche. Cependant, si vous avez modifié un grand nombre de pages, il est plus commode de mettre à jour tout à la fois au lieu de les ouvrir un par un dans le navigateur. Dans ce cas, vous pouvez reconstruire l'index de recherche manuellement.

![](https://raw.github.com/contao/docs/3.1/manual/en/images/rebuild-the-search-index.jpg)


[1]: 03-Managing-pages.md#access-control
[2]: https://contao.org/en/extension-list.html
[3]: 01-Installation.md#the-contao-install-tool
