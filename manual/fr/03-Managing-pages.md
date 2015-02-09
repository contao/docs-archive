# Gestion des pages

Les chapitres suivants expliquent comment gérer les pages dans Contao. Depuis 
que Contao est un système de gestion de contenu basé sur les pages, ces 
dernières et la structure de site sont les éléments centraux de votre site 
internet et tout contenu qui n'est pas associé à une page ne ​​pourra jamais 
être vu.


## Composants

Comprendre comment les pages, les articles, les éléments de contenu et les 
modules sont liés entre eux est la clé de l'apprentissage de Contao. Comme 
mentionné précédemment, la structure de site est l'élément central de votre 
site. Les visiteurs de votre site internet demandent toujours des pages et non 
des articles comme dans un CMS basé sur des nœuds.

![](images/composants.jpg?raw=true)

Le diagramme montre que les articles et les présentations de page sont les deux 
éléments les plus importantes d'une page. Alors que les articles stockent le 
contenu d'une page, la présentation de page définit la façon dont il est affiché 
sur le site. Les présentations de page de Contao sont basées sur les CSS et bien 
sûr elles n'utilisent pas de mise en page avec des tables. Les chapitres suivants 
expliquent comment créer des feuilles de style et des modules, comment les 
combiner dans une présentation de page et comment créer des pages qui 
l'utilisent.


## Thèmes

Bien que le gestionnaire de thèmes est une nouvelle fonctionnalité de la version 
2.9, il est en fait juste une interface améliorée pour quelque chose qui faisait 
déjà partie de Contao. Une design de site internet se compose généralement de 
feuilles de style, de modules front office, de présentations de page, de 
fichiers et de modèles que vous pouvez gérer dans le back office de Contao. Le 
gestionnaire de thème ne change pas cette approche du tout, il ajoute juste une 
option pour exporter et importer ces ressources.


### Thèmes par opposition aux modèles du front office

La principale différence entre les [thèmes][1] et les modèles du front office 
est qu'un modèle du front office contient un exemple de site internet 
entièrement préconfiguré, y compris un exemple de structure de site, d'articles, 
d'éléments de contenu et même d'utilisateurs et de groupes d'utilisateurs. Un 
thème, en revanche, ne contient que le design du site internet et peut donc être 
importé sans risque de perdre toutes les données existantes.

![](images/gestionnaire-theme.jpg?raw=true)


### Composants d'un thème

Un thème est un groupe de [feuilles de style][2], de [modules front office][3] 
et de [présentations de page][4], qui sont tous stockés dans la base de données 
et automatiquement reconnus par l'exportateur de thème. Vous en apprendrez plus 
sur ces éléments dans les chapitres suivants. Un thème inclut habituellement des 
images et d'autres fichiers à partir du répertoire des fichiers et des modèles 
personnalisés en option à partir du répertoire des modèles. Toutefois, ces 
ressources ne sont pas automatiquement liées avec le thème et doivent donc être 
ajoutées dans la configuration du thème pour y être inclues dans l'exportation.

![](images/parametres-theme.jpg?raw=true)


### Exportation et importation d'un thème

Pour exporter un thème, cliquez simplement sur le bouton d'exportation et 
télécharger le fichier .cto en local sur votre ordinateur. Bien que .cto est une 
extension de fichier propriétaire pour les thèmes de Contao, le fichier est en 
fait une archive ZIP qui peut être extraite avec chaque programme qui traite les 
fichiers .zip. Pour réimporter un thème, téléversez le fichier .cto dans votre 
installation de Contao, ouvrez le gestionnaire de thèmes et cliquez sur "Import 
de thème". Vous pouvez importer plusieurs thèmes à la fois. Une fois 
l'importation terminée, vous pouvez associer une ou plusieurs présentations de 
page du nouveau thème dans la structure de site.


## Feuilles de style

Les sites internet accessibles doivent toujours être formatés à l'aide des CSS, 
c'est pourquoi Contao inclut un module "feuilles de style" qui vous permet de 
gérer les définitions de formatage dans le back office. Pour référencer les 
différents éléments de Contao, vous devez connaître leurs noms de classe. Les 
[classes des éléments de contenu][5] commencent par "ce\_" (par exemple "ce_text") 
et les [classes des modules][3] avec "mod\_" (par exemple "mod_search"). Si vous 
n'êtes pas sûr, il suffit de regarder dans le code source de la page.

![](images/feuille-de-style.jpg?raw=true)

Chaque feuille de style peut être limitée par un ou plusieurs types de média 
et/ou par une version particulière d'Internet Explorer, dans le cas où vous avez 
besoin de fixer un de ses nombreux bogues. Faites attention à l'ordre des 
définitions de formatage, car celles qui suivent, remplacent les précédentes.

``` {.css}
/* Définir la valeur générale d'abord */
.mod_search {
    margin:24px;
}

/* Puis la remplacer pour IE7 */
*:first-child+html .mod_search {
    margin:18px;
}
```

Si l'ordre est inversé, la valeur générale l'emporterait sur la marge spécifique
à Internet Explorer.


## Modules

Les modules front office vous permettent d'ajouter presque n'importe quel type 
de fonctionnalités à votre site internet. Le cœur de Contao comprend des 
modules pour générer différents menus de navigation, gérer l'enregistrement et 
l'authentification d'un membre, rechercher sur le site, l'importation de flux 
RSS et bien plus encore. Pour créer un module, connectez-vous au back office et 
choisissez "Thèmes" -> "modules front office" dans le menu de navigation.

<table>
<tr>
  <th>Module</th>
  <th>Classe CSS</th>
  <th>Description</th>
</tr>
<tr>
  <td>Menu de navigation</td>
  <td>mod_navigation</td>
  <td>Génère un menu de navigation à partir de la structure de site.</td>
</tr>
<tr>
  <td>Navigation personnalisée</td>
  <td>mod_customnav</td>
  <td>Génère un menu personnalisé.</td>
</tr>
<tr>
  <td>Navigation "fil d'Ariane"</td>
  <td>mod_breadcrumb</td>
  <td>Génère un menu de type "fil d'Ariane".</td>
</tr>
<tr>
  <td>Navigation rapide</td>
  <td>mod_quicknav</td>
  <td>Génère un menu de type liste déroulante à partir de la structure de 
  site.</td>
</tr>
<tr>
  <td>Lien rapide</td>
  <td>mod_quicklink</td>
  <td>Génère un menu de type liste déroulante.</td>
</tr>
<tr>
  <td>Navigation "Livre"</td>
  <td>mod_booknav</td>
  <td>Génère un menu de type "Livre".</td>
</tr>
<tr>
  <td>Pagination d'articles</td>
  <td>mod_article_nav</td>
  <td>Génère une pagination pour naviguer dans les articles.</td>
</tr>
<tr>
  <td>Plan du site</td>
  <td>mod_sitemap</td>
  <td>Génère une liste de toutes les pages de la structure de site.</td>
</tr>
<tr>
  <td>Formulaire de connexion</td>
  <td>mod_login</td>
  <td>Génère un formulaire de connexion.</td>
</tr>
<tr>
  <td>Déconnexion automatique</td>
  <td>-</td>
  <td>Déconnecte automatiquement un membre.</td>
</tr>
<tr>
  <td>Données personnelles</td>
  <td>mod_personalData</td>
  <td>Génère un formulaire permettant de modifier les données personnelles 
  d'un membre.</td>
</tr>
<tr>
  <td>Formulaire d'inscription</td>
  <td>mod_registration</td>
  <td>Crée un formulaire d'inscription.</td>
</tr>
<tr>
  <td>Mot de passe perdu</td>
  <td>mod_password</td>
  <td>Crée un formulaire de demande de nouveau mot de passe.</td>
</tr>
<tr>
  <td>Fermer le compte</td>
  <td>mod_closeAccount</td>
  <td>Crée un formulaire pour supprimer le compte d'un membre.</td>
</tr>
<tr>
  <td>Liste d'actualités</td>
  <td>mod_newslist</td>
  <td>Ajoute une liste d'actualités à la page.</td>
</tr>
<tr>
  <td>Lecteur d'actualités</td>
  <td>mod_newsreader</td>
  <td>Affiche les détails d'une actualité.</td>
</tr>
<tr>
  <td>Archive d'actualités</td>
  <td>mod_newsarchive</td>
  <td>Ajoute une archive d'actualités à la page.</td>
</tr>
<tr>
  <td>Menu archive d'actualités</td>
  <td>mod_newsmenu</td>
  <td>Génère un menu de navigation pour une archive d'actualités.</td>
</tr>
<tr>
  <td>Calendrier</td>
  <td>mod_calendar</td>
  <td>Ajoute un calendrier dans une page.</td>
</tr>
<tr>
  <td>Lecteur d'événement</td>
  <td>mod_eventreader</td>
  <td>Affiche les détails d'un événement.</td>
</tr>
<tr>
  <td>Liste d'événements</td>
  <td>mod_eventlist</td>
  <td>Ajoute une liste d'événements dans une page.</td>
</tr>
<tr>
  <td>Menu liste d'événements</td>
  <td>mod_eventmenu</td>
  <td>Génère un menu de navigation pour parcourir la liste d'événements.</td>
</tr>
<tr>
  <td>S'abonner</td>
  <td>mod_subscribe</td>
  <td>Génère un formulaire pour s'abonner à une ou plusieurs listes de 
  diffusion.</td>
</tr>
<tr>
  <td>Se désabonner</td>
  <td>mod_unsubscribe</td>
  <td>Génère un formulaire pour se désabonner à une ou plusieurs listes de 
  diffusion.</td>
</tr>
<tr>
  <td>Liste de bulletins d'information</td>
  <td>mod_nl_list</td>
  <td>Ajoute une liste de bulletins d'information à une page.</td>
</tr>
<tr>
  <td>Lecteur de bulletins d'information</td>
  <td>mod_nl_reader</td>
  <td>Affiche les détails d'un bulletin d'information.</td>
</tr>
<tr>
  <td>Liste de FAQ</td>
  <td>mod_faqlist</td>
  <td>Ajoute une liste de questions fréquemment posées dans la page.</td>
</tr>
<tr>
  <td>Lecteur de FAQ</td>
  <td>mod_faqreader</td>
  <td>Affiche la réponse à une question fréquemment posée.</td>
</tr>
<tr>
  <td>Page de FAQ</td>
  <td>mod_faqpage</td>
  <td>Afficher la liste de FAQ et le lecteur de FAQ sur la même page.</td>
</tr>
<tr>
  <td>Formulaire</td>
  <td>mod_form</td>
  <td>Ajoute un formulaire dans la page.</td>
</tr>
<tr>
  <td>Moteur de recherche</td>
  <td>mod_search</td>
  <td>Ajoute un formulaire de recherche dans la page.</td>
</tr>
<tr>
  <td>Commentaires</td>
  <td>mod_comments</td>
  <td>Gérer les commentaires ou les entrées d'un livre d'or.</td>
</tr>
<tr>
  <td>Liste d'enregistrements</td>
  <td>mod_listing</td>
  <td>Lister les enregistrements d'une table de la base de données.</td>
</tr>
<tr>
  <td>Animation Flash</td>
  <td>mod_flash</td>
  <td>Permet d'inclure une animation Flash dans une page.</td>
</tr>
<tr>
  <td>Liste d'articles</td>
  <td>mod_article_list</td>
  <td>Génère une liste d'articles contenu dans une zone particulière.</td>
</tr>
<tr>
  <td>Image aléatoire</td>
  <td>mod_random_image</td>
  <td>Ajoute une image aléatoire dans une page.</td>
</tr>
<tr>
  <td>Code HTML personnalisé</td>
  <td>-</td>
  <td>Permet d'inclure du code HTML personnalisé.</td>
</tr>
<tr>
  <td>Lecteur de flux RSS</td>
  <td>mod_rss_reader</td>
  <td>Ajoute un flux RSS à la page.</td>
</tr>
</table>


### Contrôle d'accès

Chaque module front office peut être protégé de sorte que seuls les invités ou 
les membres d'un groupe en particulier puissent le voir sur le site internet.

![](images/module-protege.jpg?raw=true)


## Présentations de page

Les présentations de page déterminent l'agencement basique d'une page, par ex. 
le nombre de colonnes ou la largeur générale, et elle définissent quels modules 
de front office vont être affichés dans quelles colonnes. Elles permettent aussi 
d'inclure des feuilles de style, de lier la page à un flux RSS ou Atom, 
d'associer un ID Google Analytics et d'ajouter du code JavaScript qui pourrait 
être requis pour contrôler des éléments interactifs ou des plugins. Le framework 
CSS de Contao divise automatiquement la fenêtre du navigateur en plusieurs 
sections et affiche les modules qui ont été assignés à ces sections les uns à 
la suite des autres.

![](../en/images/front-end-structure.jpg?raw=true)

![](images/modules-front-office.jpg?raw=true)

Cela implique que lorsque vous allez créer une présentation de page, vous devriez 
déjà avoir créé toutes les feuilles de style et les modules front office que vous 
voulez inclure. C'est pourquoi, il est recommandé de créer les ressources dans 
l'ordre suivant :

* Créer les modules front office nécessaires
* Créer les feuilles de style nécessaires
* Optionnellement, créer des archives d'actualités ou des calendriers
* Créer une présentation de page et combiner tous les composants


## Types de page

Le type de page détermine si la page va afficher du contenu, rediriger vers une 
autre page ou définir le point de départ d'un nouveau site internet dans la 
structure de page. Contao supporte six types de pages différents qui sont 
expliqués ci-dessous. 

<table>
<tr>
  <th>Type de page</th>
  <th>Description</th>
</tr>
<tr>
  <td>Page simple</td>
  <td>Une page simple contient des articles et des éléments de contenu. C'est 
  le type de page par défaut.</td>
</tr>
<tr>
  <td>Rediriger vers une URL externe</td>
  <td>Ce type de page réoriente automatiquement les visiteurs vers une URL 
  externe. Cela fonctionne comme un lien hypertexte.</td>
</tr>
<tr>
  <td>Rediriger vers une autre page du site</td>
  <td>Ce type de page réoriente automatiquement les visiteurs vers une autre 
  page de la structure de site.</td>
</tr>
<tr>
  <td>Racine d'un nouveau site</td>
  <td>Ce type de page est le point de départ pour créer un site internet dans 
  la structure de site.</td>
</tr>
<tr>
  <td>Erreur 403 (accès interdit)</td>
  <td>Si un utilisateur sans permission essaye d'accéder à une page protégée, 
  une page d'erreur 403 sera retournée. Cette page doit être ajoutée <b>au 
  premier niveau</b> dans votre page racine d'un nouveau site.</td>
</tr>
<tr>
  <td>Erreur 404 (page non trouvée)</td>
  <td>Si un utilisateur essaye d'accéder à une page qui n'existe pas, une page 
  d'erreur 404 sera retournée. Cette page doit être ajoutée <b>au premier 
  niveau</b> dans votre page racine d'un nouveau site.</td>
</tr>
</table>


### Mode multi-domaines

Contao supporte plusieurs sites internet à l'intérieur de la structure de site 
et redirige automatiquement les visiteurs vers une racine de site particulière 
en fonction du nom de domaine ou des réglages de langues. Imaginons par exemple 
que vous deviez créer un site d'entreprise bilingue qui utilise le nom de 
domaine "www.example.com" et un petit site personnel qui utilise le nom de 
domaine "www.personal.example.org". Vous aurez besoin de trois pages racines 
d'un nouveau site pour cela : 

<table>
<tr>
  <th>Type</th>
  <th>DNS</th>
  <th>Code de langue</th>
  <th>Langue de secours</th>
</tr>
<tr>
  <td>Site internet d'entreprise en Allemand</td>
  <td>aucun</td>
  <td>de</td>
  <td>non</td>
</tr>
<tr>
  <td>Site internet d'entreprise en Anglais</td>
  <td>aucun</td>
  <td>en</td>
  <td>oui</td>
</tr>
<tr>
  <td>Site internet personnel</td>
  <td>www.personal.example.org</td>
  <td>de</td>
  <td>oui</td>
</tr>
</table>

Le tableau suivant montre vers quelle page un visiteur va être redirigé en 
fonction du nom de domaine et de la langue de son navigateur.

<table>
<tr>
  <th>Domaine</th>
  <th>Langue du navigateur</th>
  <th>Cible de redirection</th>
</tr>
<tr>
  <td>www.example.com</td>
  <td>Anglais</td>
  <td>Site internet d'entreprise en Anglais</td>
</tr>
<tr>
  <td>www.example.com</td>
  <td>Allemand</td>
  <td>Site internet d'entreprise en Allemand</td>
</tr>
<tr>
  <td>www.example.com</td>
  <td>Espagnol</td>
  <td>Site internet d'entreprise en Anglais</td>
</tr>
<tr>
  <td>www.personal.example.org</td>
  <td>Non pertinent</td>
  <td>Site internet personnel</td>
</tr>
</table>

Notez que si nous n'utilisions pas l'option "langue de secours", le site internet 
personnel ne serait disponible que pour les utilisateurs dont la langue du 
navigateur est l'Allemand ! 


### Droits d'accès

Les droits d'accès déterminent ce que les utilisateurs du back office sont 
autorisés à faire avec une page et ses articles. Ils n'ont rien à voir avec les 
pages protégées qui ne sont accessibles que par certains utilisateurs front 
office ! Similaire au système de permissions des fichiers Unix, il existe trois 
niveaux d'autorisation :

* Accès en tant que propriétaire d'une page
* Accès en tant que membre d'un groupe propriétaire de la page
* Accès en tant qu'utilisateur sans privilège

Chaque niveau peut avoir différentes permissions. Par défaut, le propriétaire de 
la page est autorisé à éditer la page elle-même ainsi que les articles de la 
page, tandis qu'un utilisateur d'un groupe qui possède une page est autorisé à 
éditer les articles seulement. Les utilisateurs sans privilège n'ont aucun droits 
en écriture.

![](images/droits-acces.jpg?raw=true)


[1]: https://contao.org/en/contao-themes-and-templates.html
[2]: 03-Managing-pages.md#feuilles-de-style
[3]: 03-Managing-pages.md#modules
[4]: 03-Managing-pages.md#présentations-de-page
[5]: 04-Managing-content.md#articles
