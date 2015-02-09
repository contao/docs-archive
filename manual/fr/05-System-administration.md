# Administration du système

Les chapitres suivants expliquent comment administrer Contao. Outre 
l'installation et la mise à jour de l'application, un administrateur est 
responsable de la création des utilisateurs et des groupes d'utilisateurs, 
de gérer les modules additionnels et de la maintenance du système.


## Utilisateurs et groupes d'utilisateurs

Contao fait une distinction entre les utilisateurs du back office 
("utilisateurs"), qui peuvent se connecter au panneau d'administration, et les 
utilisateurs front office ("membres"), qui peuvent se connecter au site 
internet. Contrairement aux administrateurs, qui ont accès à toutes les pages 
et à tous les éléments par défaut ("allow all"), les utilisateurs ne peuvent 
pas accéder à une ressource qui n'a pas été explicitement autorisée dans leur 
profil ou dans le profil de l'un des groupes d'utilisateurs auxquels ils 
appartiennent ("deny all").


### Utilisateurs

Chaque utilisateur peut être associé à plusieurs groupes d'utilisateurs et 
hérite automatiquement de leurs autorisations. Toutes les autorisations sont 
cumulatives, ce qui signifie que l'utilisateur hérite de la somme des 
permissions de tous les groupes auxquels il appartient. Si le groupe A accorde 
un certain droit, vous ne pouvez pas la révoquer dans le groupe B.


#### Pages autorisées

L'option "Pages autorisées" permet de définir quelles pages de la structure de 
site, l'utilisateur est autorisé à voir. La capture d'écran ci-dessous montre 
la structure de site telle qu'elle est perçue par Helen Lewis. Bien que le site 
internet contient beaucoup plus de pages, elle ne peut en voir que trois, parce 
que seul l'accès à la page "Courses" a été autorisé dans les paramètres du 
groupe "Editors". Notez que même si Helen Lewis est autorisée à voir trois 
pages, elle ne peut modifier que l'une d'elles !

![](images/site-structure-hlewis-fr.jpg?raw=true)

Être capable de voir une page n'inclut pas le droit de la modifier (ou de 
modifier ses articles). Rappelez-vous que [les permissions d'une page][1] sont 
définies dans la structure de site, donc pour permettre l'accès à une page à un 
utilisateur, vous devez la sélectionner dans son profil et accorder son accès 
dans la structure de site.


#### Répertoires autorisés

Semblable à l'option "Pages autorisées", l'option "Répertoires autorisés" définie 
quels répertoires un utilisateur est autorisé à voir. La capture d'écran 
ci-dessous montre le gestionnaire de fichiers tel qu'il est perçu par Helen Lewis. 
Elle n'est autorisée de voir que le répertoire "campus", alors que les 
administrateurs peuvent voir le répertoire complet des fichiers (`files`).

![](images/gestionnaire-fichiers-hlewis.jpg?raw=true)


#### Champs autorisés

Comme mentionné au début, les utilisateurs n'ont pas du tout de permissions par 
défaut ("deny all"), ce qui implique aussi qu'ils ne peuvent pas accéder aux 
champs d'un formulaire. Même s'ils sont par exemple autorisés à accéder au 
module d'actualités, le formulaire pour créer une nouvelle entrée sera vide 
jusqu'à ce que l'administrateur sélectionne un ou plusieurs champs de la table 
`tl_news` dans les paramètres du groupe.

![](images/champs-autorises.jpg?raw=true)


### Membres

La gestion des membres (utilisateurs front office) est beaucoup plus facile à
gérer que celle des utilisateurs back office, car il n'y a pas de pages ou de
champs à autoriser. La gestion des membres est principalement requise pour
contrôler l'accès aux pages protégées, qui est mis en œuvre au niveau du groupe.
En fonction de la configuration du site internet, les membres inscrits pourront 
voir des pages protégées ou accéder à des téléchargements protégés qui ne sont 
pas disponibles pour les invités.


## Extensions

Les extensions sont une partie essentielle de Contao, car ils vous permettent 
d'ajouter des fonctionnalités supplémentaires. Il existe plus de 1400 extensions 
disponibles dans le référentiel d'extensions de Contao, que vous pouvez parcourir 
directement à partir du back office. La communication avec le serveur du 
référentiel s'effectue via SOAP, donc vous devez activer l'extension SOAP de PHP 
pour utiliser le service (si elle n'est pas activée par défaut).


### Catalogue d'extensions

Le module "Catalogue d'extensions" vous permet de parcourir la liste des 
extensions et d'installer des extensions par simple pression d'un bouton. 
Utilisez les options de filtrage et de tri pour trouver une extension 
particulière et cliquez sur l'icône d'information ou le titre de l'extension 
pour ouvrir la page de détails et installer le module.

![](images/liste-extension.jpg?raw=true)

La page de détails contient une description de l'extension et des informations 
importantes concernant les configurations du système requises ainsi que les 
versions et les dépendances d'autres modules. Cliquez sur le bouton "Installer" 
pour télécharger et installer l'extension.

![](images/details-extension.jpg?raw=true)

Contao téléchargera et installera automatiquement l'extension et mettra à jour 
la base de données si nécessaire.

![](images/installer-extension.jpg?raw=true)


### Gestionnaire d'extensions

Le module "Gestionnaire d'extensions" vous permet de mettre à jour et de 
désinstaller des extensions. Il vérifie automatiquement les mises à jour et 
vous avertit si une nouvelle version est disponible. De nombreuses extensions 
incluent également des liens vers un manuel en ligne et/ou un fil de discussion 
dans un forum où vous pouvez obtenir de l'aide.

![](images/gestionnaire-extension.jpg?raw=true)

Pour désinstaller une extension, cliquez simplement sur l'icône de 
désinstallation et suivez les instructions. Le gestionnaire d'extensions va 
supprimer tous les fichiers et répertoires et mettre à jour la base de données 
si nécessaire. Notez que cette action ne peut pas être annulée et les tables ne 
peuvent pas être restaurées !

![](images/desinstaller-extension.jpg?raw=true)


### Installation manuelle

Dans le cas où l'extension SOAP de PHP n'est pas disponible sur votre serveur, 
vous pouvez également installer des extensions de Contao manuellement. Trouvez 
le module correspondant dans la [liste des extensions][2] et téléchargez 
l'archive .zip de la dernière version. Ensuite, décompressez les fichiers et 
copiez-les dans votre répertoire local ou distant de Contao. Enfin, vérifiez 
la base de données avec l'[outil d'installation de Contao][3].


## Maintenance

La plupart des travaux d'entretien dans Contao sont exécutés automatiquement par 
le "Periodic Command Scheduler", vous pouvez donc vous concentrer sur votre 
travail. Même les tâches dans le module de maintenance sont effectuées 
automatiquement, mais parfois il est nécessaire de les déclencher manuellement.


### Purger des données

Outre le contenu généré par l'utilisateur, Contao stocke beaucoup de données du 
système qui sont utilisées pour restaurer les enregistrements supprimés, revenir 
à des versions antérieures, créer l'index de recherche du site internet ou 
réduire le temps de chargement d'une page. Vous pouvez purger ces données 
manuellement par exemple pour supprimer les anciennes vignettes à partir du 
cache d'images ou pour recréer les fichiers XML du plan du site après que vous 
ayez modifié la structure de site.

![](images/nettoyer-donnees.jpg?raw=true)


### Reconstruire l'index de recherche

Les pages sont généralement ajoutées automatiquement à l'index de recherche 
quand elles sont vues dans le front office (sauf si vous êtes connecté au back 
office en même temps), vous n'avez donc pas besoin de vous inquiéter au sujet 
de l'index de recherche. Cependant, si vous avez modifié un grand nombre de 
pages, il est plus commode de les mettre à jour toutes à la fois au lieu de les 
ouvrir une par une dans le navigateur. Dans ce cas, vous pouvez reconstruire 
l'index de recherche manuellement.

![](images/recreer-recherche-index.jpg?raw=true)


[1]: 03-Managing-pages.md#contrôle-daccès
[2]: https://contao.org/en/extension-list.html
[3]: 01-Installation.md#loutil-dinstallation-de-contao
