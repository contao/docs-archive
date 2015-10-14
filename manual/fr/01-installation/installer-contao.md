## Installer Contao

Premièrement, veuillez télécharger la [dernière archive de Contao][1] et
l'extraire sur votre ordinateur. Déplacez les fichiers dans le répertoire
`htdocs` de votre installation locale (par exemple XAMPP) ou les téléverser sur
votre serveur avec un logiciel FTP (nous vous recommandons d'utiliser
[WinSCP][2]). Selon la configuration de votre serveur, le dossier public est
probablement nommé `htdocs`, `httpdocs`, `html` ou `public_html`.

Si vous avez un accès SSH, vous pouvez télécharger et extraire l'archive avec
les commandes suivantes:

```bash
curl -L http://download.contao.org | tar -xzp
```


### Installation avec Composer

Vous pouvez également installer Contao avec Composer en utilisant le référentiel
[contao/standard-edition][6].

```bash
php composer.phar create-project contao/standard-edition <target>
```

Vous devez remplacer le paramètre `<target>` avec un chemin d'accès vers un
dossier où les fichiers de Contao seront créés. Si le dossier cible n'existe
pas, il sera créé automatiquement.

En premier lieu, avant d'exécuter cette commande, vous devez
[installer Composer][7]. Il peut être installé globalement avec les deux
commandes suivantes sur Mac OS X ou Linux:

```bash
curl -sS https://getcomposer.org/installer | php
sudo mv composer.phar /usr/local/bin/composer
```

Sous Windows, vous pouvez télécharger et exécuter le
[programme d'installation][10].

Lors de l'installation dans votre interface en ligne de commande, vous devez
affecter une valeur à un certain nombre de paramètres :

```bash
Some parameters are missing. Please provide them.
database_host (localhost):
database_port (3306):
database_user (null):
database_password (null):
database_name (null):
mailer_transport (mail):
mailer_host (127.0.0.1):
mailer_user (null):
mailer_password (null):
mailer_port (25):
mailer_encryption (null):
prepend_locale (false):
secret (ThisTokenIsNotSoSecretChangeIt):
```

Les valeurs par défaut sont listées entre parenthèses. Toutes ces données seront
incluses dans le fichier de configuration `app/config/parameters.yml`.

Le paramètre `secret` vous permet de créer une clé qui sera utilisée contre les
attaques [CSRF][8]. Il est très important de prendre le temps de créer une clé
forte. Comme décrit dans la documentation de Symfony :

> **Information** Sa valeur doit être une série de caractères, chiffres et
symboles choisis au hasard et la longueur recommandée est d'environ 32 caractères.

Vous pouvez trouver plus d'informations sur cette configuration sur le
[site officiel de Symfony][9].


### L'outil d'installation de Contao

Pour ouvrir l'outil d'installation de Contao, il suffit d'ajouter
`/contao/install.php` à l'URL de votre installation de Contao. Notez que l'outil
d'installation est protégé contre les attaques par force brute et sera bloqué si
un mauvais mot de passe a été inséré trois fois de suite. Pour enlever le verrou,
ouvrez le fichier `system/config/localconfig.php` dans un éditeur de texte,
trouvez la ligne ci-dessous et définissez-là à `0`.

```php
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
nouvelle et [*officielle démonstration de Contao*][3] ou l'ancienne
[*Music Academy*][4] peuvent être installées en tant qu'extension.
Les informations concernant la compatibilité sont disponibles dans le
référentiel d'extensions.

**Comment installer le modèle de démonstration :**

1. Créer une nouvelle installation de Contao avec un compte administrateur
2. S'identifier en tant qu'administrateur dans le back office
3. Installer l'extension correspondante [en utilisant le référentiel d'extensions][5]
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


[1]: https://contao.org/en/download.html
[2]: http://www.winscp.net/
[3]: https://contao.org/en/extension-list/view/official_demo.en.html
[4]: https://contao.org/en/extension-list/view/music_academy.en.html
[5]: ../05-administration-du-systeme/extensions.md#catalogue-d-extensions
[6]: https://github.com/contao/standard-edition
[7]: https://getcomposer.org/download/
[8]: https://fr.wikipedia.org/wiki/Cross-Site_Request_Forgery
[9]: http://symfony.com/doc/current/reference/configuration/framework.html#secret
[10]: https://getcomposer.org/doc/00-intro.md#using-the-installer
