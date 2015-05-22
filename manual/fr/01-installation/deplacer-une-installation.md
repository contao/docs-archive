## Déplacer une installation

Déplacer une installation de Contao à partir d'un serveur local vers un serveur
en ligne n'est pas très différent de l'installation d'une nouvelle version de
Contao, à l'exception que vous utilisez les fichiers de votre installation
locale au lieu d'une archive de Contao et une sauvegarde SQL de votre base de
données locale.


### Téléverser les fichiers

Ouvrez votre logiciel FTP, connectez-vous au serveur cible et téléverser tous
les fichiers de votre installation locale de Contao.


### Exportation de la base de données

La façon la plus simple de créer une sauvegarde MySQL est d'utiliser l'outil
d'administration de bases de données "phpMyAdmin". Si vous êtes un
administrateur du serveur, vous pouvez également utiliser l'utilitaire
`mysqldump` bien sûr. Connectez-vous à "phpMyAdmin", choisissez la base de
données que vous souhaitez exporter et cliquez sur l'onglet "Exporter" dans le
menu supérieur. Il est important d'ajuster les paramètres d'exportation
conformément à la capture d'écran ci-dessous afin de restreindre les problèmes
de compatibilité de versions de MySQL.

![](images/sql-export.jpg)


### Importation de la base de données

Ouvrez "phpMyAdmin" sur le serveur cible et créez une nouvelle base de données
pour Contao. En fonction de la configuration du serveur, vous devrez
probablement utiliser le panneau d'administration du serveur (par exemple,
"Plesk" ou "cPanel") pour créer de nouvelles bases de données. Sélectionnez la
base de données vide et cliquez sur l'onglet "Importer" dans le menu supérieur.
Puis télécharger la sauvegarde SQL de votre base de données locale et lancez
l'importation.

![](images/sql-import.jpg)


### Ajustement de la configuration de la base de données

Enfin, ouvrez l'outil d'installation de Contao de la nouvelle installation
(le mot de passe doit être le même que pour votre installation locale) et
ajustez la configuration de la base de données si nécessaire. Ensuite, allez au
panneau d'administration et connectez-vous avec votre nom d'utilisateur et
votre mot de passe.
