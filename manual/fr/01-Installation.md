# Installation

Les chapitres suivants expliquent comment installer et mettre à jour Contao. Vous
apprendrez à utiliser l'outil d'installation de Contao, comment synchroniser une 
installation existante via FTP, comment configurer le "Safe Mode Hack" ainsi 
qu'un serveur pour Contao.


## Installer Contao

Premièrement, veuillez télécharger la [dernière archive de Contao][1] et 
l'extraire sur votre ordinateur. Déplacez les fichiers dans le répertoire 
`htdocs` de votre installation locale (par exemple XAMPP) ou les téléverser sur 
votre serveur avec un logiciel FTP (nous vous recommandons d'utiliser 
[WinSCP][2]). Selon la configuration de votre serveur, le dossier public est 
probablement nommé `htdocs`, `httpdocs`, `html` ou `public_html`.

Si vous avez un accès SSH, vous pouvez télécharger et extraire l'archive avec 
les commandes suivantes:

``` {.bash}
curl -L http://download.contao.org | tar -xzp
```


### L'outil d'installation de Contao

Pour ouvrir l'outil d'installation de Contao, il suffit d'ajouter 
`/contao/install.php` à l'URL de votre installation de Contao. Notez que l'outil 
d'installation est protégé contre les attaques par force brute et sera bloqué si
un mauvais mot de passe a été inséré trois fois de suite. Pour enlever le verrou,
ouvrez le fichier `system/config/localconfig.php` dans un éditeur de texte, 
trouvez la ligne ci-dessous et définissez-là à `0`.

``` {.php}
$GLOBALS['TL_CONFIG']['installCount'] = 0; // Ceci enlèvera le verrouillage automatique
```


#### Connexion à la base de données

Connectez-vous au panneau d'administration de votre serveur (par exemple "Plesk"
ou "cPanel") et créez une nouvelle base de données pour Contao. Ensuite, entrez
les identifiants de connexion dans l'outil d'installation de Contao. Notez que
le jeu de caractères par défaut de Contao `UTF-8` s'écrit `UTF8` dans MySQL !


#### Mise à jour des tables de la base de données

Lorsque que vous êtes connecté à la base de données, Contao vérifie
automatiquement ses tables et affiche une liste de changements recommandés dans
le cas où ils ne seraient pas à jour. Assurez-vous de lire attentivement ces 
recommandations, car Contao ne connaît que ses propres tables et tentera de 
supprimer celles d'autres applications en partage avec la base de données. 
Confirmez les modifications et cliquez sur le bouton "Mettre à jour la base 
de données".


#### Importer un modèle

Un modèle est un site internet pré-configuré qui comprend un exemple de
structure de site et plusieurs feuilles de style pour formater les modules de
base de Contao ainsi que les éléments de contenu.

A partir de la version 3.2.11, le site internet de démonstration n'est plus
inclus dans le package de téléchargement. Selon la version utilisée, la
nouvelle et [*officielle démonstration de Contao*][12] ou l'ancienne
[*Music Academy*][13] peuvent être installées en tant qu'extension.
Les informations concernant la compatibilité sont disponibles dans le
référentiel d'extensions.

**Comment installer le modèle de démonstration :**

1. Créer une nouvelle installation de Contao avec un compte administrateur
2. S'identifier en tant qu'administrateur dans le back office
3. Installer l'extension correspondante [en utilisant le référentiel d'extensions][14]
4. Se déconnecter du back office
5. Ouvrir de nouveau l'outil d'installation

Pour importer un modèle, sélectionnez l'entrée dans le menu déroulant
et cliquez sur le bouton "Importer un modèle".

**Les données existantes seront remplacées lors de l'importation d'un modèle !**


#### Création d'un utilisateur administrateur

Si vous n'avez pas importé un modèle, vous devez créer un utilisateur
administrateur pour se connecter au back office de Contao. Après avoir créé le
compte, le processus d'installation est terminé. Le lien dans le coin inférieur 
droit vous amènera vers le panneau d'administration. Si vous avez importé le site 
internet d'exemple, vous pouvez vous connecter en tant qu'utilisateur "k.jones" 
avec le mot de passe "kevinjones".


### Installation du modèle de démonstration de Contao

Voir *Comment installer le modèle de démonstration* dans la section
*Importer un modèle*


### Utiliser des URLs conviviales pour les moteurs de recherche

Si vous utilisez un serveur Apache et êtes autorisé à utiliser mod_rewrite, vous 
pouvez faire en sorte que Contao génère des URLs conviviales pour les moteurs de 
recherche qui ressemblent à des documents HTML statiques. Un ensemble de règles 
de réécriture par défaut est stocké dans le fichier `.htaccess.default` situé 
dans le répertoire de Contao. Renommez ce fichier en `.htaccess` afin que le 
serveur Apache puisse le traiter, puis connectez-vous au back office et accédez 
à la configuration du système. Sélectionnez "Ré-écrire les URLs" dans la section 
"Configuration du front office" et enregistrez vos modifications. Maintenant, 
Contao génère des URLs statiques comme `home.html` au lieu de `index.php?id=12`.


## Utilisation du Safe Mode Hack

En essayant d'installer Contao avec l'outil d'installation, vous pourriez voir 
un avertissement que le fichier de configuration local n'est pas accessible en 
écriture.

![](../en/images/localconfig-not-writable.jpg?raw=true)


### Problèmes d'autorisation de fichiers

Le terme «Safe Mode Hack» peut prêter à confusion, car il implique que le 
problème a été causé par le `safe_mode` de PHP. Cependant, il est causé par des 
permissions de fichiers insuffisantes et peut se produire même si le `safe_mode` 
est désactivé, il devrait donc être appelé "File Permission Hack" à la place. 
PHP en tant que module Apache est généralement exécuté comme `wwwrun`, `www-data`
ou `nobody`, alors que les fichiers que vous téléverser via FTP vous 
appartiennent (par exemple `web4` ou `ab5678`). Le serveur refuse donc, au 
script PHP de Contao, l'accès à ces fichiers.


#### Utilisation du FTP pour les opérations sur les fichiers

Pour contourner le problème des permissions, Contao établit une connexion FTP 
pour modifier les fichiers et les répertoires. Tout ce que vous avez à faire est 
d'entrer vos identifiants de connexion FTP. Faites attention lorsque vous entrez
le chemin relatif à partir de votre répertoire racine FTP vers le répertoire de 
Contao (par exemple `html/`, `public_html/` ou `httpdocs/`).

Quelques répertoires nécessitent encore des autorisations d'écriture, car PHP va 
y accéder directement :

* `assets/images`
* `assets/images/*`
* `system/logs`
* `system/tmp`

Les permissions (CHMOD 777) sont fixées automatiquement par l'outil 
d'installation et n'ont normalement pas à être ajustées manuellement. Si cela 
est nécessaire, veuillez s'il vous plaît **seulement n'ajuster que les trois 
répertoires mentionnés ci-dessus** - et cela en dépit de ce que vous pourriez 
avoir lu dans un tutoriel ou dans les forums de Contao !


## Mise à jour manuelle

Pour mettre à jour manuellement une installation de Contao, vous pouvez soit 
téléverser l'archive complète de Contao sur le serveur (remplacement des 
fichiers) ou vous pouvez téléverser uniquement les fichiers qui ont été 
modifiés depuis la dernière mise à jour (synchronisation des fichiers). De 
toute façon, vous devriez toujours sauvegarder les fichiers et dossiers 
ci-dessous juste au cas où il y aurait une erreur ou lors d'un remplacement 
accidentel :

* `files/*`
* `system/config/dcaconfig.php`
* `system/config/initconfig.php`
* `system/config/langconfig.php`
* `system/config/localconfig.php`
* `templates/*`

Cela permettra de sauvegarder votre configuration locale, vos modèles 
personnalisés et vos fichiers.


### Remplacement de fichiers

Le remplacement des fichiers d'une installation de Contao est assez simple. Il 
suffit de décompresser l'archive de Contao sur le serveur ou de l'extraire sur 
votre ordinateur et de téléverser les fichiers avec un client FTP. Puis, 
restaurer les fichiers que vous avez sauvegardés et enlever les éventuels 
fichiers inutilisés des versions antérieures de Contao.

**Attention:** Si vous avez installé des extensions tierces, assurez-vous de 
les sauvegarder et de les restaurer eux aussi, ou ne les effacer pas du tout. 
Sinon, vous devrez réinstaller les modules et, en fonction de l'extension, 
vous pourriez finir par perdre des données !


### Synchronisation de fichiers

Pour synchroniser une installation de Contao, vous pouvez soit utiliser 
l'[utilitaire Unix diff][3] ou un logiciel FTP. Les utilitaires Unix sont 
généralement utilisés par les administrateurs de serveurs uniquement et, par 
conséquent, ils ne seront pas expliqués ici. Pour synchroniser des fichiers via 
FTP, ouvrez WinSCP et connectez-vous au serveur. Sauvegardez les fichiers 
mentionnés ci-dessus, puis accédez au répertoire de Contao et cliquez sur le 
bouton "Synchroniser les fichiers".

![](../en/images/synchronization-options.jpg?raw=true)

Contrôlez les options attentivement et assurez-vous de choisir "Preview changes" 
pour que vous puissiez contrôler quels fichiers seront mis à jour. Ensuite 
confirmez chaque fichier dans la fenêtre d'aperçu et contrôlez spécialement les 
fichiers qui vont être effacés ! Cliquez sur OK pour démarrer le processus de 
synchronisation. 

![](../en/images/synchronization-confirmation.jpg?raw=true)


### Mise à jour de la base de données

Après avoir mis à jour les fichiers de Contao, vous devez également mettre à jour 
la base de données. Heureusement, l'outil d'installation de Contao effectuera le 
gros du travail pour vous. Il suffit de l'ouvrir et de saisir votre mot de passe, 
puis faites défiler la page vers le bas jusqu'à la section base de données et 
confirmez les modifications.


### Purger le cache interne

Finalement, vous devez également reconstruire le cache interne (pour les DCA et
les fichiers de langue). Dans le back office, allez à "Maintenance du système"
et cochez "Purger le cache interne" dans la section "Nettoyer les données".
Confirmez l'action en cliquant sur "Nettoyer les données".

Vous recevrez un message dans l'en-tête demandant de reconstruire le cache
interne. Cliquez sur "Construire le cache" pour mettre en cache les fichiers
internes.


## Live Update Service

Le "Contao Live Update Service" est un service commercial proposé par [iNet 
Robots][4], la compagnie du fondateur de Contao et développeur principal, Leo 
Feyer. Il vous permet de mettre à jour votre installation en quelques clics à 
partir du panneau d'administration, sans avoir à télécharger une archive de 
Contao ou en utilisant un logiciel FTP pour remplacer ou synchroniser des 
fichiers.

[S'inscrire pour obtenir un ID Live Update][5]

Le Live Update comprend les fonctionnalités suivantes:

* Mise à jour et retour à une version antérieure vers n'importe quelle version 
de Contao
* Sauvegarde automatique de la base de données avant la mise à jour
* Validation personnalisée et achèvement de l'installation de Contao
* Comparaison des modèles personnalisés et des fichiers originaux


### Sélection d'une version

![](../en/images/live-update-1.jpg?raw=true)


### Différences entre les modèles

![](../en/images/live-update-2.jpg?raw=true)


### Résolution de problèmes

99% de tous les problèmes de mise à jour du Live Update sont causés par des 
permissions de fichiers erronés. Contao requiert des autorisations d'écriture 
pour gérer les fichiers et les dossiers, en conséquence si le Live Update ne 
fonctionne pas correctement, vérifiez la configuration de votre serveur et 
assurez-vous de mettre en place le Safe Mode Hack **tel que décrit dans ce mode 
d'emploi** !


#### Comment obtenir de l'aide

Si vous rencontrez des problèmes pour activer votre ID Live Update ou pour 
recevoir l'archive de mise à jour, veuillez s'il vous plaît contacter le 
[support de iNet Robots][6]. Si vous rencontrez des problèmes pour configurer 
le "Safe Mode Hack" ou pour utiliser Contao, choisissez s'il vous plaît une 
option de support sur ​​la [page de support][7].


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

![](../en/images/sql-export.jpg?raw=true)


### Importation de la base de données

Ouvrez "phpMyAdmin" sur le serveur cible et créez une nouvelle base de données 
pour Contao. En fonction de la configuration du serveur, vous devrez 
probablement utiliser le panneau d'administration du serveur (par exemple, 
"Plesk" ou "cPanel") pour créer de nouvelles bases de données. Sélectionnez la 
base de données vide et cliquez sur l'onglet "Importer" dans le menu supérieur. 
Puis télécharger la sauvegarde SQL de votre base de données locale et lancez 
l'importation.

![](../en/images/sql-import.jpg?raw=true)


### Ajustement de la configuration de la base de données

Enfin, ouvrez l'outil d'installation de Contao de la nouvelle installation 
(le mot de passe doit être le même que pour votre installation locale) et 
ajustez la configuration de la base de données si nécessaire. Ensuite, allez au 
panneau d'administration et connectez-vous avec votre nom d'utilisateur et 
votre mot de passe.


## Configuration du serveur en ligne

Ce chapitre ne traite pas sur la configuration d'un serveur en termes 
d'installation d'Apache ou de compilation de PHP, que vous ne pouvez pas faire 
sur un compte d'hébergement mutualisé de toute façon. Il explique comment 
vérifier si les exigences du système de Contao sont remplies et comment 
activer PHP 5.


### Configurations du système requises de Contao

Contao requiert un serveur web comme Apache ou IIS avec PHP et le support de 
MySQL. La version minimum de PHP est 5.3.2 et la version minimale de MySQL est 
4.1, cependant, nous vous recommandons d'utiliser MySQL 5 pour une meilleure 
performance. Vous avez également besoin des extensions PHP "GDlib" 
(redimensionnement d'image), "DOM" (fichiers XML) et "SOAP" (référentiel 
d'extensions) et éventuellement "mbstring" (gestion des caractères multi-octets) 
ainsi que "mcrypt" (cryptage des données). Contao a été testé avec succès avec 
tous les principaux navigateurs comme Firefox (à partir de la version 2) ou 
Internet Explorer (à partir de la version 8).


### Contao Check

Télécharger "Contao Check" afin de savoir si votre serveur répond aux exigences
du système de Contao. Le script va vérifier si vous pouvez utiliser le 
référentiel d'extensions ainsi que le "Live Update" et si vous devez utiliser le 
"Safe Mode Hack" ou non. Selon la configuration de votre système, vous pouvez 
mettre en place une nouvelle installation de Contao avec l'installateur web ou 
valider une installation existante.

![](images/contao-check-fr.jpg?raw=true)

Extrayez le fichier Zip, téléversez le dossier `check` dans votre répertoire 
d'installation de Contao et ouvrez-le dans un navigateur Web.

[Télécharger Contao Check][8] | [Ouvrir le projet sur GitHub][9]


### Paramètres FAI spécifiques

Il y a quelques grands fournisseurs d'accès à internet qui requièrent un peu de 
configurations supplémentaires afin que Contao puisse fonctionner. Heureusement, 
ils ne sont que l'exception qui confirme la règle. Les paramètres FAI 
spécifiques sont décrites dans le [forum de Contao][10]. Si vous cherchez un 
hébergement sans tracas pour Contao, consultez la liste des [hébergements 
partenaires de Contao][11].


[1]: https://contao.org/en/download.html
[2]: http://www.winscp.com/
[3]: http://fr.wikipedia.org/wiki/Diff
[4]: http://www.inetrobots.com
[5]: http://www.inetrobots.com/shop/product_info.php?info=p12_Live-Update-ID.html
[6]: http://www.inetrobots.com/contact-us.html
[7]: https://contao.org/en/support.html
[8]: https://github.com/contao/check/zipball/master
[9]: https://github.com/contao/check
[10]: https://community.contao.org/en/
[11]: https://contao.org/en/partners.html?search=services&for=partner_hosting
[12]: https://contao.org/en/extension-list/view/official_demo.en.html
[13]: https://contao.org/en/extension-list/view/music_academy.en.html
[14]: 05-System-administration.md#catalogue-dextensions