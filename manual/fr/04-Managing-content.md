# Gestion du contenu

Les chapitres suivants expliquent comment gérer le contenu dans Contao. Le cœur 
de Contao supporte de nombreux types de contenu comme des articles, des 
actualités, des événements, des bulletins d'information, des formulaires ou des 
définitions. D'autres types de contenu comme des bannières, des billets, des 
produits ou des recommandations sont disponibles dans le [référentiel 
d'extensions][1]. Pour créer du contenu, se connecter au back office et choisir 
un des modules dans la section "Contenu" du menu de navigation.


## Articles

Les articles sont des conteneurs pour les éléments de contenu. Regrouper les 
éléments de contenu par article rend le travail plus facile pour déplacer, 
publier, copier, éditer ou exporter ces éléments ensemble au lieu d'un par un. 
Chaque article est associé à une page particulière et à une section particulière 
de cette page, il a ainsi une position fixe dans la structure de site et sur le 
site internet. Contao peut optionnellement n'afficher qu'une accroche d'article 
avec un lien "En savoir plus...".


### Éléments de contenu

Les éléments de contenu sont un moyen simple et intuitif pour créer du contenu. 
Au lieu d'utiliser un éditeur de texte riche, Contao fournit un élément 
distinct pour chaque type de contenu comme les textes, les listes, les 
tableaux, les liens hypertextes, les images ou les téléchargements. Voici un 
aperçu des éléments de contenu de base de Contao :

<table>
<tr>
  <th>Nom</th>
  <th>Classe CSS</th>
  <th>Description</th>
</tr>
<tr>
  <td>Titre</td>
  <td>ce_headline</td>
  <td>Génère un titre (h1 - h6).</td>
</tr>
<tr>
  <td>Texte</td>
  <td>ce_text</td>
  <td>Génère un texte enrichi qui peut être formaté à l'aide de 
  <a href="http://www.tinymce.com">TinyMCE</a>.</td>
</tr>
<tr>
  <td>HTML</td>
  <td>-</td>
  <td>Vous permet d'ajouter du code HTML personnalisé.</td>
</tr>
<tr>
  <td>Liste</td>
  <td>ce_list</td>
  <td>Génère une liste ordonné ou non ordonnée.</td>
</tr>
<tr>
  <td>Tableau</td>
  <td>ce_table</td>
  <td>Génère un tableau qui peut-être trié.</td>
</tr>
<tr>
  <td>Code</td>
  <td>ce_code</td>
  <td>Ajoute la coloration syntaxique sur des extraits de code et les 
  imprime sur l'écran.</td>
</tr>
<tr>
  <td>Accordéon (élément seul)</td>
  <td>ce_accordion</td>
  <td>Génère un seul élément accordéon (avec <a href="http://mootools.net">
  MooTools</a>).</td>
</tr>
<tr>
  <td>Accordéon (début de l'enveloppe)</td>
  <td>ce_accordionStart</td>
  <td>Génère l'ouverture du conteneur de l'accordéon.</td>
</tr>
<tr>
  <td>Accordéon (fin de l'enveloppe)</td>
  <td>-</td>
  <td>Génère la fermeture du conteneur de l'accordéon.</td>
</tr>
<tr>
  <td>Slider de contenu (début de l'enveloppe)</td>
  <td>ce_sliderStart</td>
  <td>Génère l'ouverture du conteneur du slider.</td>
</tr>
<tr>
  <td>Slider de contenu (fin de l'enveloppe)</td>
  <td>-</td>
  <td>Génère la fermeture du conteneur du slider.</td>
</tr>
<tr>
  <td>Lien hypertexte</td>
  <td>ce_hyperlink</td>
  <td>Génère un lien hypertexte vers un autre site internet.</td>
</tr>
<tr>
  <td>Lien vers le haut de page</td>
  <td>ce_toplink</td>
  <td>Génère un lien pour retourner en haut de page.</td>
</tr>
<tr>
  <td>Image</td>
  <td>ce_image</td>
  <td>Génère une image.</td>
</tr>
<tr>
  <td>Galerie d'images</td>
  <td>ce_gallery</td>
  <td>Génère une galerie d'images avec effet 
  <a href="http://www.digitalia.be/software/slimbox">lightbox</a>.</td>
</tr>
<tr>
  <td>Vidéo/audio</td>
  <td>ce_player</td>
  <td>Génère un lecteur vidéo ou audio.</td>
</tr>
<tr>
  <td>YouTube</td>
  <td>ce_youtube</td>
  <td>Ajoute une vidéo YouTube.</td>
</tr>
<tr>
  <td>Téléchargement</td>
  <td>ce_download</td>
  <td>Génère un lien hypertexte vers un fichier à télécharger.</td>
</tr>
<tr>
  <td>Téléchargements</td>
  <td>ce_downloads</td>
  <td>Génère des liens hypertextes multiples vers des fichiers à télécharger.
  </td>
</tr>
<tr>
  <td>Contenu d'un article</td>
  <td>-</td>
  <td>Insère un autre article.</td>
</tr>
<tr>
  <td>Élément de contenu</td>
  <td>(classe parente)</td>
  <td>Insère un autre élément de contenu.</td>
</tr>
<tr>
  <td>Formulaire</td>
  <td>ce_form</td>
  <td>Insère un formulaire.</td>
</tr>
<tr>
  <td>Module</td>
  <td>(classe parente)</td>
  <td>Insère un module front office.</td>
</tr>
<tr>
  <td>Accroche d'un article</td>
  <td>ce_teaser</td>
  <td>Affiche l'accroche d'un article.</td>
</tr>
<tr>
  <td>Commentaires</td>
  <td>ce_comments</td>
  <td>Ajouter un formulaire de saisie de commentaires à la page.</td>
</tr>
</table>


### Contrôle d'accès

Chaque élément de contenu peut être protégé de sorte que seuls les invités 
ou les membres d'un groupe en particulier puissent le voir sur le site 
internet.

![](https://raw.github.com/contao/docs/3.1/manual/en/images/protected-element.jpg)


### Contenu Flash

Le contenu Flash est un type particulier de contenu qui n'est pas affiché dans 
un article sur le site internet mais chargé dans un film Flash dynamique en 
utilisant "loadVars()". Pour permettre la communication entre Contao et Flash, 
vous devez ajouter la fonction suivante au frame principal de votre film :


``` {.as}
TextField.prototype._loadArticle = function(flashID) {
  tf = this;

  // Autoriser le mode HTML et supprimer le contenu
  tf.html = true;
  tf.htmlText = "";

  // Instancier un nouvel objet LoadVars
  lv = new LoadVars();
  lv["flashID"] = flashID;
  lv.sendAndLoad(URL + "flash.php", lv, "POST");

  lv.onLoad = function(success) {
    if (success) {
      tf.htmlText = lv["content"];
    }
  }
}

// Charger le contenu Flash "myArticle" dans le champ texte "myTextBox"
myTextBox._loadArticle("myArticle");
```


#### Importer une feuille de style

Le code ActionScript suivant vous permet d'importer une feuille de style 
pour formater un champ de texte dynamique :


``` {.as}
TextField.prototype._addCSS = function(style_sheet) {
  tf= this;
  tf.styleSheet = null;

  // Instancier un nouvel objet StyleSheet
  st = new TextField.StyleSheet();
  st.load(URL + style_sheet);

  st.onLoad = function(success) {
    if (success) {
      tf.styleSheet = st;
    }
  }
}

// Ajouter la feuille de style "basic.css" au champ texte "myTextBox"
myTextBox._addCSS("basic.css");
```

Notez que Flash ne prend en charge qu'un petit sous-ensemble de balises HTML, 
de sorte que certains de vos styles puissent ne pas s'afficher correctement.


## Actualités

L'extension actualités/blog vous permet de gérer des actualités ou des billets 
d'un blog et de les afficher dans le front office. Contrairement aux articles 
qui sont associés à une page en particulier, les actualités sont organisées 
dans des archives d'actualités, qui vous permet de facilement les regrouper, 
de les catégoriser ou de les exporter.


### Archives d'actualités

Les archives d'actualité sont utilisées pour regrouper et/ou catégoriser les 
actualités. Chaque archive peut se rapporter à une certaine langue ou un sujet 
particulier.


### Modules front office

Les modules front office sont utilisés pour afficher les actualités sur le site 
internet. Ils peuvent être configurés avec le module "Modules" dans le back 
office et doivent être ajoutés à un article ou à une présentation de page pour 
pouvoir apparaître sur le site internet. L'extension actualités/blog comprend 
quatre modules front office :

<table>
<tr>
  <th>Module</th>
  <th>Classe CSS</th>
  <th>Description</th>
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
  <td>mod_newsarchiveMenu</td>
  <td>Génère un menu de navigation pour une archive d'actualités.</td>
</tr>
</table>


### Permaliens

Chaque actualité a une URL unique (permalien) qui peut être utilisée pour 
la référencer :

```
http://www.domain.com/news/items/james-wilson-returns.html
```

L'URL ci-dessus sollicite l'actualité "james-Wilson-retours" via la page 
"actualités". Rappelez-vous que Contao est un CMS basé sur les pages, donc si 
la page "actualités" n'existait pas ou si elle ne comprenait pas le module 
lecteur d'actualités, alors l'actualité ne serait pas affichée.


## Événements

L'extension calendrier vous permet de gérer des événements et de les afficher 
dans un calendrier ou une liste d'événements sur le site internet. Contrairement 
aux articles qui sont associés à une page en particulier, les événements sont 
organisés dans des calendriers, qui vous permet de les regrouper, de les classer 
ou de les exporter.


### Calendriers

Les calendriers sont utilisés pour regrouper et/ou catégoriser des événements. 
Chaque calendrier peut se rapporter à une certaine langue ou un sujet 
particulier.


### Modules front office

Les Modules front office sont utilisés pour afficher des événements sur le 
site internet. Ils peuvent être configurés avec le module "Modules" dans le 
back office et doivent être ajoutés à un article ou à une présentation de 
page pour pouvoir apparaître sur le site internet. L'extension calendrier 
comprend quatre modules front office :

<table>
<tr>
  <th>Module</th>
  <th>Classe CSS</th>
  <th>Description</th>
</tr>
<tr>
  <td>Calendrier</td>
  <td>mod_calendar</td>
  <td>Ajoute un calendrier dans une page.</td>
</tr>
<tr>
  <td>Lecteur d'événements</td>
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

</table>


### Permaliens

Chaque événement a une URL unique (permalien) qui peut être utilisée pour le 
référencer :

```
http://www.domain.com/event-reader/events/final-exams.html
```

L'URL ci-dessus sollicite l'événement "final-exams" via la page "events". 
Rappelez-vous que Contao est un CMS basé sur les pages, donc si la page "events" 
n'existait pas ou si elle n'incluait pas le module lecteur d'événements, alors
l'événement ne serait pas affiché. 


## Flux RSS/Atom

Cette fonctionnalité peut être utilisée pour les archives d'actualités et les 
calendriers. Voici un exemple avec la liste des calendriers.

![](https://raw.github.com/contao/docs/3.1/manual/en/images/rss-calendar.jpg)


### Paramètres

Un ou plusieurs calendriers peuvent être regroupés et exportés en tant que flux 
RSS ou Atom. Il en va de même pour les archives d'actualités. Dans un même 
temps, vous pouvez choisir d'exporter uniquement les accroches ou les articles 
complets de chaque événement ou actualité.

![](https://raw.github.com/contao/docs/3.1/manual/en/images/rss-settings.jpg)


### Fichiers XML

Les fichiers XML sont générés automatiquement dans le répertoire ```share``` 
de votre installation de Contao. Dans cet exemple : ```share/events.xml```.


## Bulletins d'information

L'extension bulletins d'information vous permet de gérer et d'envoyer des 
bulletins d'information et optionnellement de les afficher sur le site 
internet. Contrairement aux articles qui sont associés à une page particulière, 
les bulletins d'information sont organisés en listes de diffusion, ce qui vous 
permet de facilement les regrouper ou de les catégoriser.


### Destinataires

Les inscriptions à un bulletin d'information sont traitées par les modules front 
office créés à cet effet, donc vous n'avez pas à gérer les destinataires 
manuellement. Pour des raisons de protection des données privées, Contao utilise 
l'inscription par [Double Opt In][2] et ne stocke que l'adresse e-mail de 
l'abonné.

![](https://raw.github.com/contao/docs/3.1/manual/en/images/newsletter-recipients.jpg)

Au cas où vous auriez déjà une liste de destinataires, vous pouvez l'importer 
dans Contao à partir d'un fichier CSV.


### Bulletins d'information personnalisés

Dans la mesure où vous envoyez des bulletins d'information à des membres 
inscrits, vous pouvez personnaliser ces bulletins avec des "Simple Tokens". 
Les "Simple Tokens" fonctionnent d'une manière similaire à celle des [balises 
d'insertion][3] et peuvent être utilisés aussi bien dans la version HTML que 
dans la version texte de votre bulletin d'information.

```
Cher ##firstname## ##lastname##,

Veuillez mettre à jour vos données personnelles :

Rue:         ##street## 
Code postal: ##postal##
Ville:       ##city##
Téléphone:   ##phone## 
E-mail:      ##email## 

L'administrateur
```

Cependant, contrairement aux balises d'insertion, les "Simple Tokens" ne 
permettent pas seulement d'ajouter des données de la table `tl_member`, mais 
aussi de faire des déclarations if-else simples, par ex. de spécifier une 
salutation : 

```
{if gender=="male"}
Monsieur ##lastname##,
{elseif gender=="female"}
Madame ##lastname##,
{else}
Madame, Monsieur,
{endif}

[contenu du bulletin]

{if phone==""}
Veuillez s'il vous plaît mettre à jour vos informations de contact et entrer 
votre numéro de téléphone.
{endif}

L'administrateur
```


### Envoyer des bulletins d'information

En particulier sur les hébergements mutualisés, il y a des limites concernant 
le temps d'exécution d'un script et/ou le nombre d'e-mails qui peuvent être 
envoyés par minute. Contao essaie de contourner ces deux problèmes en divisant 
le processus d'envoi en plusieurs cycles pour éviter le dépassement du temps 
d'exécution du script et en ajoutant une pause entre chaque cycle pour 
contrôler le nombre d'e-mails par minute.

![](https://raw.github.com/contao/docs/3.1/manual/en/images/sending-newsletters.jpg)


### Modules front office

Les modules front office sont utilisés pour gérer les inscriptions aux 
bulletins d'information et optionnellement les afficher sur le site internet. 
Ils peuvent être configurés avec le module "Modules" dans le back office et 
doivent être ajoutés à un article ou à une présentation de page pour être 
affichés sur le site internet.

<table>
<tr>
  <th>Module</th>
  <th>Classe CSS</th>
  <th>Description</th>
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
</table>


### Permaliens

Chaque bulletin d'information a une URL unique (permalien) qui peut être 
utilisée pour le référencer :

```
http://www.domain.com/newsletters/items/james-wilson-returns.html
```

L'URL ci-dessus sollicite le bulletin d'information "james-wilson-returns" via 
la page "newsletters". Rappelez-vous que Contao est un CMS basé sur les pages, 
donc si la page "newsletters" n'existait pas ou si elle n'incluait pas le 
module lecteur de bulletins d'information, alors le bulletin d'information ne 
serait pas affiché. 


## Formulaires

Le générateur de formulaire intégré peut être utilisé pour créer des 
formulaires interactifs qui sont envoyées via e-mail ou stockés dans la base 
de données de Contao. Les fichiers téléversés peuvent être envoyés en tant 
que pièces jointes par e-mail ou stockés dans le répertoire des fichiers de 
Contao. Le générateur de formulaire prend en charge quatre formats de données 
différents :

<table>
<tr>
  <th>Format</th>
  <th>Description</th>
</tr>
<tr>
  <td>Raw data</td>
  <td>Les données du formulaire sont envoyées comme du simple texte avec une 
  nouvelle ligne pour chaque champ.</td>
</tr>
<tr>
  <td>XML file</td>
  <td>Les données du formulaire sont envoyées en pièce jointe sous la forme 
  d'un fichier XML.</td>
</tr>
<tr>
  <td>CSV file</td>
  <td>Les données du formulaire sont envoyées en pièce jointe sous la forme 
  d'un fichier CSV.</td>
</tr>
<tr>
  <td>E-mail</td>
  <td>Tous les champs sont ignorés à part email, subject, message et cc (copie 
  carbone) et les données sont envoyées comme si l'e-mail avait été envoyé 
  depuis un client de messagerie. Les envois de fichiers sont autorisés.</td>
</tr>
</table>


### Les champs du formulaire

Semblable aux éléments de contenu, Contao propose un élément séparé pour chaque 
type de champ de formulaire tels que les champs de textes, les champs de mots 
de passe, les menus déroulants, les téléchargements de fichiers, les champs 
cachés ou boutons de soumission. Voici un aperçu des champs disponibles de 
Contao :

<table>
<tr>
  <th>Champ</th>
  <th>Classe CSS</th>
  <th>Description</th>
</tr>
<tr>
  <td>Titre</td>
  <td>headline</td>
  <td>Champ personnalisé pour insérer un titre de section.</td>
</tr>
<tr>
  <td>Explication</td>
  <td>explanation</td>
  <td>Champ personnalisé pour insérer un texte d'explication.</td>
</tr>
<tr>
  <td>Code HTML</td>
  <td>-</td>
  <td>Champ personnalisé pour insérer du code HTML.</td>
</tr>
<tr>
  <td>Fieldset</td>
  <td>-</td>
  <td>Un conteneur pour les champs avec une légende en option (uniquement 
  disponible pour les formulaires sans tableau).</td>
</tr>
<tr>
  <td>Champ texte</td>
  <td>text</td>
  <td>Champ d'une ligne pour la saisie d'un texte court ou moyen.</td>
</tr>
<tr>
  <td>Champ mot de passe</td>
  <td>password</td>
  <td>Champ d'une ligne pour la saisie d'un mot de passe. Contao ajoute 
  automatiquement un champ de confirmation.</td>
</tr>
<tr>
  <td>Zone de texte</td>
  <td>textarea</td>
  <td>Champ comportant plusieurs lignes pour la saisie d'un texte moyen ou 
  long.</td>
</tr>
<tr>
  <td>Liste déroulante</td>
  <td>select/multiselect</td>
  <td>Liste déroulante pour la sélection d'un ou plusieurs choix.</td>
</tr>
<tr>
  <td>Bouton radio</td>
  <td>radio</td>
  <td>Liste de plusieurs options dont une seule peut être sélectionnée.</td>
</tr>
<tr>
  <td>Case à cocher</td>
  <td>checkbox</td>
  <td>Liste de plusieurs options dont chacune peut être sélectionnée.</td>
</tr>
<tr>
  <td>Envoi de fichier</td>
  <td>upload</td>
  <td>Champ d'une ligne pour l'envoi d'un fichier local vers le serveur.</td>
</tr>
<tr>
  <td>Champ caché</td>
  <td>-</td>
  <td>Champ d'une ligne non visible dans le formulaire.</td>
</tr>
<tr>
  <td>Question de sécurité</td>
  <td>captcha</td>
  <td>Question simple d'arithmétique pour vérifier que le formulaire est bien 
  soumis par un individu (CAPTCHA).</td>
</tr>
<tr>
  <td>Bouton d'envoi</td>
  <td>submit</td>
  <td>Bouton d'envoi du formulaire.</td>
</tr>
</table>


## Balises d'insertion

Les balises d'insertion sont des jokers qui sont remplacés par du contenu 
dynamique quand une page est affichée à l'écran. Elles vous permettent, par 
exemple, d'afficher la date courante, l'adresse d'un membre en fonction de 
son nom ou bien d'inclure un fichier. Les balises d'insertion peuvent être 
utilisées presque partout dans Contao, même dans les pages en cache.


### Les éléments de lien

Les balises d'insertion suivantes vous permettent de faire un lien vers une 
autre page ou vers un article en utilisant son ID ou son alias.

<table>
<tr>
  <th>Balise d'insertion</th>
  <th>Description</th>
</tr>
<tr>
  <td><code>{{link::*}}</code></td>
  <td>Cette balise sera remplacée par un lien vers une page interne (remplacez 
  * par un ID ou un alias de page).</td>
</tr>
<tr>
  <td><code>{{link::back}}</code></td>
  <td>Cette balise sera remplacée par un lien vers la dernière page visitée. 
  Peut aussi être utilisée avec "link_open", "link_url" et "link_title".</td>
</tr>
<tr>
  <td><code>{{link::login}}</code></td>
  <td>Cette balise sera remplacée par un lien vers la page de connexion du 
  membre actuellement connecté (s'il y en a un).</td>
</tr>
<tr>
  <td><code>{{link_open::*}}</code></td>
  <td>Cette balise sera remplacée par la balise d'ouverture d'un lien vers une 
  page interne : <code>{{link_open::12}}Cliquez ici{{link_close}}</code>.</td>
</tr>
<tr>
  <td><code>{{link_url::*}}</code></td>
  <td>Cette balise sera remplacée par l'URL d'une page interne : <code>&lt;a 
  href="{{link_url::12}}">Cliquez ici&lt;/a&gt;</code>.</td>
</tr>
<tr>
  <td><code>{{link_title::*}}</code></td>
  <td>Cette balise sera remplacée par le titre d'une page interne : <code>&lt;a 
  title="{{link_title::12}}">Cliquez ici&lt;/a&gt;</code>.</td>
</tr>
<tr>
  <td><code>{{link_close}}</code></td>
  <td>Cette balise sera remplacée par la balise de fermeture d'un lien vers une 
  page interne : <code>{{link_open::12}}Cliquez ici{{link_close}}</code>.</td>
</tr>
<tr>
  <td><code>{{article::*}}</code></td>
  <td>Cette balise sera remplacée par un lien vers un article (remplacez * par 
  un ID ou un alias d'article).</td>
</tr>
<tr>
  <td><code>{{article_open::*}}</code></td>
  <td>Cette balise sera remplacé par la balise d'ouverture du lien vers un 
  article : <code>{{article_open::12}}Cliquez ici{{link_close}}</code>.</td>
</tr>
<tr>
  <td><code>{{article_url::*}}</code></td>
  <td>Cette balise sera remplacée par l'URL d'un article : <code>&lt;a
      href="{{article_url::12}}">Cliquez ici&lt;/a&gt;</code>.</td>
</tr>
<tr>
  <td><code>{{article_title::*}}</code></td>
  <td>Cette balise sera remplacée par le titre d'un article : <code>&lt;a
      title="{{article_title::12}}">Cliquez ici&lt;/a&gt;</code>.</td>
</tr>
<tr>
  <td><code>{{news::*}}</code></td>
  <td>Cette balise sera remplacée par un lien vers une actualité (remplacez * 
  par un ID ou un alias d'actualité).</td>
</tr>
<tr>
  <td><code>{{news_open::*}}</code></td>
  <td>Cette balise sera remplacé par la balise d'ouverture du lien vers une 
  actualité : <code>{{news_open::12}}Cliquez ici{{link_close}}</code>.</td>
</tr>
<tr>
  <td><code>{{news_url::*}}</code></td>
  <td>Cette balise sera remplacée par l'URL d'une actualité : <code>&lt;a
      href="{{news_url::12}}">Cliquez ici&lt;/a&gt;</code>.</td>
</tr>
<tr>
  <td><code>{{news_title::*}}</code></td>
  <td>Cette balise sera remplacée par le titre d'une actualité : <code>&lt;a
      title="{{news_title::12}}">Cliquez ici&lt;/a&gt;</code>.</td>
</tr>
<tr>
  <td><code>{{event::*}}</code></td>
  <td>Cette balise sera remplacée par un lien vers un événement (remplacez * 
  par un ID ou un alias d'événement).</td>
</tr>
<tr>
  <td><code>{{event_open::*}}</code></td>
  <td>Cette balise sera remplacé par la balise d'ouverture du lien vers un 
  événement : <code>{{event_open::12}}Cliquez ici{{link_close}}</code>.</td>
</tr>
<tr>
  <td><code>{{event_url::*}}</code></td>
  <td>Cette balise sera remplacée par l'URL d'un événement : <code>&lt;a
      href="{{event_url::12}}">Cliquez ici&lt;/a&gt;</code>.</td>
</tr>
<tr>
  <td><code>{{event_title::*}}</code></td>
  <td>Cette balise sera remplacée par le titre d'un événement : <code>&lt;a
      title="{{event_title::12}}">Cliquez ici&lt;/a&gt;</code>.</td>
</tr>
<tr>
  <td><code>{{faq::*}}</code></td>
  <td>Cette balise sera remplacée par un lien vers une question fréquemment 
  posée (remplacez * par un ID ou un alias de FAQ).</td>
</tr>
<tr>
  <td><code>{{faq_open::*}}</code></td>
  <td>Cette balise sera remplacé par la balise d'ouverture du lien d'une 
  question : <code>{{faq_open::12}}Cliquez ici{{link_close}}</code>.</td>
</tr>
<tr>
  <td><code>{{faq_url::*}}</code></td>
  <td>Cette balise sera remplacée par l'URL d'une question : <code>&lt;a 
  href="{{faq_url::12}}">Cliquez ici&lt;/a&gt;</code>.</td>
</tr>
<tr>
  <td><code>{{faq_title::*}}</code></td>
  <td>Cette balise sera remplacée par le titre d'une question : <code>&lt;a
      title="{{faq_title::12}}">Cliquez ici&lt;/a&gt;</code>.</td>
</tr>
</table>


### Propriétés de l'utilisateur

Les balises d'insertion suivantes vous permettent d'afficher n'importe quelle 
propriété du membre actuellement connecté. 

<table>
<tr>
  <th>Balise d'insertion</th>
  <th>Description</th>
</tr>
<tr>
  <td><code>{{user::firstname}}</code></td>
  <td>Cette balise sera remplacée par le prénom du membre actuellement 
  connecté.</td>
</tr>
<tr>
  <td><code>{{user::lastname}}</code></td>
  <td>Cette balise sera remplacée par le nom de famille du membre actuellement 
  connecté.</td>
</tr>
<tr>
  <td><code>{{user::company}}</code></td>
  <td>Cette balise sera remplacée par le nom de la société du membre 
  actuellement connecté.</td>
</tr>
<tr>
  <td><code>{{user::phone}}</code></td>
  <td>Cette balise sera remplacée par le n° de téléphone du membre actuellement 
  connecté.</td>
</tr>
<tr>
  <td><code>{{user::mobile}}</code></td>
  <td>Cette balise sera remplacée par le n° de téléphone portable du membre 
  actuellement connecté.</td>
</tr>
<tr>
  <td><code>{{user::fax}}</code></td>
  <td>Cette balise sera remplacée par le n° de fax du membre actuellement 
  connecté.</td>
</tr>
<tr>
  <td><code>{{user::email}}</code></td>
  <td>Cette balise sera remplacée par l'adresse e-mail du membre actuellement 
  connecté.</td>
</tr>
<tr>
  <td><code>{{user::website}}</code></td>
  <td>Cette balise sera remplacée par l'adresse du site internet du membre 
  actuellement connecté.</td>
</tr>
<tr>
  <td><code>{{user::street}}</code></td>
  <td>Cette balise sera remplacée par le nom de la rue du membre actuellement 
  connecté.</td>
</tr>
<tr>
  <td><code>{{user::postal}}</code></td>
  <td>Cette balise sera remplacée par le code postal du membre actuellement 
  connecté.</td>
</tr>
<tr>
  <td><code>{{user::city}}</code></td>
  <td>Cette balise sera remplacée par le nom de la ville du membre 
  actuellement connecté.</td>
</tr>
<tr>
  <td><code>{{user::country}}</code></td>
  <td>Sera remplacée par le nom du pays du membre actuellement connecté.</td>
</tr>
<tr>
  <td><code>{{user::username}}</code></td>
  <td>Cette balise sera remplacée par le nom d'utilisateur du membre 
  actuellement connecté.</td>
</tr>
</table>


### Propriétés de page

Les balises d'insertion suivantes vous permettent d'afficher n'importe quelle 
propriété de la page courante. 

<table>
<tr>
  <th>Balise d'insertion</th>
  <th>Description</th>
</tr>
<tr>
  <td><code>{{page::id}}</code></td>
  <td>Cette balise sera remplacée par l'ID de la page courante.</td>
</tr>
<tr>
  <td><code>{{page::alias}}</code></td>
  <td>Cette balise sera remplacée par l'alias de la page courante.</td>
</tr>
<tr>
  <td><code>{{page::title}}</code></td>
  <td>Cette balise sera remplacée par le nom de la page courante.</td>
</tr>
<tr>
  <td><code>{{page::pageTitle}}</code></td>
  <td>Cette balise sera remplacée par le titre de la page courante.</td>
</tr>
<tr>
  <td><code>{{page::language}}</code></td>
  <td>Cette balise sera remplacée par la langue de la page courante.</td>
</tr>
<tr>
  <td><code>{{page::parentAlias}}</code></td>
  <td>Cette balise sera remplacée par l'alias de la page parente.</td>
</tr>
<tr>
  <td><code>{{page::parentTitle}}</code></td>
  <td>Cette balise sera remplacée par le nom de la page parente.</td>
</tr>
<tr>
  <td><code>{{page::parentPageTitle}}</code></td>
  <td>Cette balise sera remplacée par le titre de la page parente.</td>
</tr>
<tr>
  <td><code>{{page::mainAlias}}</code></td>
  <td>Cette balise sera remplacée par l'alias de la page parente principale.
  </td>
</tr>
<tr>
  <td><code>{{page::mainTitle}}</code></td>
  <td>Cette balise sera remplacée par le nom de la page parente principale.
  </td>
</tr>
<tr>
  <td><code>{{page::mainPageTitle}}</code></td>
  <td>Cette balise sera remplacée par le titre de la page parente principale.
  </td>
</tr>
<tr>
  <td><code>{{page::rootTitle}}</code></td>
  <td>Cette balise sera remplacée par le titre du site internet.</td>
</tr>
</table>


### Variables d'environnement

Les balises d'insertion suivantes vous permettent d'afficher les variables 
d'environnement comme le nom de la page ou la chaîne de requête. 

<table>
<tr>
  <th>Balise d'insertion</th>
  <th>Description</th>
</tr>
<tr>
  <td><code>{{env::host}}</code></td>
  <td>Cette balise sera remplacée par le nom d'hôte actuel.</td>
</tr>
<tr>
  <td><code>{{env::url}}</code></td>
  <td>Cette balise sera remplacée par le nom d'hôte et le protocole.</td>
</tr>
<tr>
  <td><code>{{env::path}}</code></td>
  <td>Cette balise sera remplacée par la base de l'URL actuelle incluant 
  le chemin vers le dossier Contao.</td>
</tr>
<tr>
  <td><code>{{env::request}}</code></td>
  <td>Cette balise sera remplacée par la chaîne de requête actuelle.</td>
</tr>
<tr>
  <td><code>{{env::ip}}</code></td>
  <td>Cette balise sera remplacée par l'adresse IP du visiteur actuel.</td>
</tr>
<tr>
  <td><code>{{env::referer}}</code></td>
  <td>Cette balise sera remplacée par l'URL de la dernière page visitée.</td>
</tr>
<tr>
  <td><code>{{env::files_url}}</code></td>
  <td>Cette balise sera remplacée par l'URL statique du répertoire files.</td>
</tr>
<tr>
  <td><code>{{env::script_url}}</code></td>
  <td>Cette balise sera remplacée par l'URL statique du répertoire scripts.
  </td>
</tr>
<tr>
  <td><code>{{env::plugins_url}}</code></td>
  <td>Cette balise sera remplacée par l'URL statique du répertoire plugins.
  </td>
</tr>
</table>


### Éléments inclus

Les balises d'insertion suivantes vous permettent d'inclure différentes 
ressources comme des articles, des modules ou des fichiers qui se trouvent dans 
le répertoire "templates". 

<table>
<tr>
  <th>Balise d'insertion</th>
  <th>Description</th>
</tr>
<tr>
  <td><code>{{insert_article::*}}</code></td>
  <td>Cette balise sera remplacée par l'article référencé (remplacez * par l'ID 
  ou l'alias de l'article).</td>
</tr>
<tr>
  <td><code>{{insert_content::*}}</code></td>
  <td>Cette balise sera remplacée par l'élément de contenu référencé (remplacez 
  * par l'ID de l'élément).</td>
</tr>
<tr>
  <td><code>{{insert_module::*}}</code></td>
  <td>Cette balise sera remplacée par le module référencé (remplacez * par l'ID 
  du module).</td>
</tr>
<tr>
  <td><code>{{article_teaser::*}}</code></td>
  <td>Cette balise sera remplacée par une accroche d'article (remplacez * par 
  l'ID de l'article).</td>
</tr>
<tr>
  <td><code>{{news_teaser::*}}</code></td>
  <td>Cette balise sera remplacée par une accroche d'actualité (remplacez * par 
  l'ID de l'actualité).</td>
</tr>
<tr>
  <td><code>{{event_teaser::*}}</code></td>
  <td>Cette balise sera remplacée par une accroche d'évènement (remplacez * par 
  l'ID de l'évènement).</td>
</tr>
<tr>
  <td><code>{{file::*}}</code></td>
  <td>Cette balise sera remplacée par le contenu d'un fichier se trouvant dans 
  le dossier "templates" (remplacez * par le nom du fichier). Vous pouvez aussi 
  fournir des arguments : <code>{{file::file.php?arg1=val&amp;arg2=val}}</code>.
  </td>
</tr>
</table>


### Divers

Les balises d'insertion suivantes vous permettent d'effectuer différentes 
tâches comme ajouter la date courante ou ajouter des images lightbox.

<table>
<tr>
  <th>Balise d'insertion</th>
  <th>Description</th>
</tr>
<tr>
  <td><code>{{date}}</code></td>
  <td>Cette balise sera remplacée par la date courante dans le format de date 
  global.</td>
</tr>
<tr>
  <td><code>{{date::*}}</code></td>
  <td>Cette balise sera remplacée par la date courante dans un format de date 
  personnalisé.</td>
</tr>
<tr>
  <td><code>{{last_update}}</code></td>
  <td>Cette balise sera remplacée par la date de la dernière mise à jour dans 
  le format de date global.</td>
</tr>
<tr>
  <td><code>{{last_update::*}}</code></td>
  <td>Cette balise sera remplacée par la date de la dernière mise à jour dans 
  un format de date personnalisé.</td>
</tr>
<tr>
  <td><code>{{email::*}}</code></td>
  <td>Cette balise sera remplacée un lien cliquable et encodé vers une adresse 
  e-mail.</td>
</tr>
<tr>
  <td><code>{{email_open::*}}</code></td>
  <td>Cette balise sera remplacée par un lien cliquable et encodé vers une 
  adresse e-mail. Toutefois, la balise de fermeture <code>&lt;/a&gt;</code> 
  ne sera pas ajoutée.</td>
</tr>
<tr>
  <td><code>{{email_url::*}}</code></td>
  <td>Cette balise sera remplacée par l'adresse e-mail encodée seulement.</td>
</tr>
<tr>
  <td><code>{{lang::*}}</code></td>
  <td>Cette balise peut être utilisée pour marquer les mots étrangers à 
  l'intérieur d'un texte : <code>{{lang::en}}Goodbye{{lang}}</code> sera 
  remplacé par <code>&lt;span lang="en" xml:lang="en"&gt;Goodbye&lt;/span&gt;
  </code>.</td>
</tr>
<tr>
  <td><code>{{abbr::*}}</code></td>
  <td>Marque les abréviations dans un texte : <code>{{abbr::World Wide Web}}WWW
  {{abbr}}</code> sera remplacé par <code>&lt;abbr title="World Wide Web"&gt;
  WWW&lt;/abbr&gt;</code>.</td>
</tr>
<tr>
  <td><code>{{acronym::*}}</code></td>
  <td>Marque les acronymes dans un texte : <code>{{acronym::Multipurpose 
  Internet Mail Extensions}}MIME{{acronym}}</code> sera remplacé par <code>&lt;
  acronym title="Multipurpose Internet Mail Extensions"&gt;MIME&lt;/acronym&gt;
  </code>.</td>
</tr>
<tr>
  <td><code>{{ua::*}}</code></td>
  <td>Propriétés de sortie de l'agent utilisateur : <code>{{ua::browser}}</code>. 
  Elle sera, par exemple, remplacée par "chrome".</td>
</tr>
<tr>
  <td><code>{{iflng::*}}</code></td>
  <td>Cette balise sera complètement supprimée si la langue de la page ne 
  correspond pas à la langue de la balise. Vous pouvez l'utiliser pour définir 
  des labels spécifiques à une langue : 
  <code>{{iflng::en}}Your name{{iflng}}{{iflng::de}}Ihr Name{{iflng}}</code>.
  </td>
</tr>
<tr>
  <td><code>{{ifnlng::*}}</code></td>
  <td>Cette balise sera complètement supprimée si la langue de la page 
  correspond à la langue de la balise. Vous pouvez l'utiliser pour définir des 
  labels spécifiques à une langue : 
  <code>{{ifnlng::de}}Your name{{iflng}}{{iflng::de}} Ihr Name{{iflng}}</code>.
  </td>
</tr>
<tr>
  <td><code>{{image::*}}</code></td>
  <td>Cette balise sera remplacée par une vignette d'image : 
      <code>{{image::files/image.jpg?width=200&amp;height=150}}</code>.<br />
      <strong>width</strong>: Largeur de la vignette,<br />
      <strong>height</strong>: Hauteur de la vignette,<br />
      <strong>alt</strong>: Texte alternatif,<br />
      <strong>class</strong>: Classe CSS,<br />
      <strong>rel</strong>: Attribut rel (par ex. "lightbox"),<br />
      <strong>mode</strong>: Mode ("proportional", "crop" ou "box").</td>
</tr>
<tr>
  <td><code>{{label::*}}</code></td>
  <td>Cette balise sera remplacée par un libellé traduit : <code>{{label::CNT:
  au}}</code> ou <code>{{label::tl_article:title:0}}</code>. Notez que seul le 
  premier deux-points est doublé.</td>
</tr>
<tr>
  <td><code>{{version::*}}</code></td>
  <td>Cette balise sera remplacée par la version actuelle de Contao (par exemple 
  2.11.2).</td>
</tr>
<tr>
  <td><code>{{request_token::*}}</code></td>
  <td>Cette balise sera remplacée par la demande de jeton de la session en cours.
  </td>
</tr>
<tr>
  <td><code>{{toggle_view}}</code></td>
  <td>Ajoute le lien qui vous permet de basculer entre le modèle pour mobile et 
  celui d'un ordinateur de bureau.</td>
</tr>
</table>


### Drapeaux des balises d'insertion

En utilisant des drapeaux, les balises d'insertion peuvent être traitées de 
manière plus approfondie. Par exemple, la valeur peut être transmise aux 
méthodes PHP spécifiques. Plusieurs drapeaux peuvent être appliqués :

```
{{ua::browser|uncached}}  
{{page::title|decodeEntities|strtoupper}}
```

Drapeaux disponibles :

<table>
<tr>
    <th>Drapeau</th>
    <th>Description</th>
    <th>Plus d'information</th>
</tr>
<tr>
    <td><code>uncached</code></td>
    <td>Ne pas remplacer une balise d'insertion lorsque la page est mise en 
    cache</td>
    <td></td>
</tr>
<tr>
    <td><code>refresh</code></td>
    <td>Ne pas mettre en cache la balise d'insertion, même si elle est utilisée 
    plusieurs fois sur la même page</td>
    <td></td>
</tr>
<tr>
    <td><code>addslashes</code></td>
    <td>Ajoute des barres obliques inversées dans une chaîne</td>
    <td><a target="_blank" href="http://php.net/addslashes">Fonction PHP</a>
    </td>
</tr>
<tr>
    <td><code>stripslashes</code></td>
    <td>Supprime les barres obliques inversées d'une chaîne</td>
    <td><a target="_blank" href="http://php.net/stripslashes">Fonction PHP</a>
    </td>
</tr>
<tr>
    <td><code>standardize</code></td>
    <td>Normalise la sortie (par exemple pour un alias de page ou une classe 
    CSS)</td>
    <td></td>
</tr>
<tr>
    <td><code>ampersand</code></td>
    <td>Convertit les esperluettes en entités de caractère HTML</td>
    <td></td>
</tr>
<tr>
    <td><code>specialchars</code></td>
    <td>Convertit les caractères spéciaux en entités de caractère HTML</td>
    <td></td>
</tr>
<tr>
    <td><code>nl2br</code></td>
    <td>Insère des retours à la ligne HTML à chaque nouvelle ligne dans une 
    chaîne</td>
    <td><a target="_blank" href="http://php.net/nl2br">Fonction PHP</a></td>
</tr>
<tr>
    <td><code>nl2br_pre</code></td>
    <td>Identique à nl2br, mais conserve les retours à la ligne dans la balise 
    <code>&lt;pre&gt;</code></td>
    <td></td>
</tr>
<tr>
    <td><code>strtolower</code></td>
    <td>Renvoie une chaîne en minuscules</td>
    <td><a target="_blank" href="http://php.net/strtolower">Fonction PHP</a>
    </td>
</tr>
<tr>
    <td><code>utf8_strtolower</code></td>
    <td>Conversion Unicode en minuscules</td>
    <td></td>
</tr>
<tr>
    <td><code>strtoupper</code></td>
    <td>Renvoie une chaîne en majuscules</td>
    <td><a target="_blank" href="http://php.net/strtoupper">Fonction PHP</a>
    </td>
</tr>
<tr>
    <td><code>utf8_strtoupper</code></td>
    <td>Conversion Unicode en majuscules</td>
    <td></td>
</tr>
<tr>
    <td><code>ucfirst</code></td>
    <td>Met le premier caractère d'une chaîne en majuscule</td>
    <td><a target="_blank" href="http://php.net/ucfirst">Fonction PHP</a></td>
</tr>
<tr>
    <td><code>lcfirst</code></td>
    <td>Met le premier caractère d'une chaîne en minuscule</td>
    <td><a target="_blank" href="http://php.net/lcfirst">Fonction PHP</a></td>
</tr>
<tr>
    <td><code>ucwords</code></td>
    <td>Met en majuscule la première lettre de tous les mots dans une chaîne
    </td>
    <td><a target="_blank" href="http://php.net/ucwords">Fonction PHP</a></td>
</tr>
<tr>
    <td><code>trim</code></td>
    <td>Supprime les espaces en début et fin de chaîne</td>
    <td><a target="_blank" href="http://php.net/trim">Fonction PHP</a></td>
</tr>
<tr>
    <td><code>rtrim</code></td>
    <td>Supprime les espaces de fin de chaîne</td>
    <td><a target="_blank" href="http://php.net/rtrim">Fonction PHP</a></td>
</tr>
<tr>
    <td><code>ltrim</code></td>
    <td>Supprime les espaces de début de chaîne</td>
    <td><a target="_blank" href="http://php.net/ltrim">Fonction PHP</a></td>
</tr>
<tr>
    <td><code>utf8_romanize</code></td>
    <td>Romanise la sortie</td>
    <td></td>
</tr>
<tr>
    <td><code>strrev</code></td>
    <td>Inverse une chaîne</td>
    <td><a target="_blank" href="http://php.net/strrev">Fonction PHP</a></td>
</tr>
<tr>
    <td><code>encodeEmail</code></td>
    <td>Encode les adresses e-mail dans la sortie</td>
    <td>see <code>String::encodeEmail</code></td>
</tr>
<tr>
    <td><code>decodeEntities</code></td>
    <td>Décode les entités de caractère HTML dans la sortie</td>
    <td>see <code>String::decodeEntities()</code></td>
</tr>
<tr>
    <td><code>number_format</code></td>
    <td>Formate un numéro (sans décimale)</td>
    <td>see <code>System::getFormattedNumber()</code></td>
</tr>
<tr>
    <td><code>currency_format</code></td>
    <td>Formate une devise (deux décimales)</td>
    <td>see <code>System::getFormattedNumber()</code></td>
</tr>
<tr>
    <td><code>readable_size</code></td>
    <td>Convertit des tailles de fichiers dans un format lisible par 
    un humain</td>
    <td>see <code>System::getReadableSize()</code></td>
</tr>
<tr>
    <td><code>base64_encode</code></td>
    <td>Encode un texte en utilisant l'<a href="http://fr.wikipedia.org/wiki/
    Base64" target="_blank">algorithme base64</a>.</td>
    <td><a target="_blank" href="http://php.net/base64_encode">Fonction PHP
    </a></td>
</tr>
<tr>
    <td><code>base64_decode</code></td>
    <td>Décode un texte en utilisant l'<a href="http://fr.wikipedia.org/wiki/
    Base64" target="_blank">algorithme base64</a>.</td>
    <td><a target="_blank" href="http://php.net/base64_decode">Fonction PHP
    </a></td>
</tr>
</table>


[1]: https://contao.org/en/extension-list.html
[2]: http://fr.wikipedia.org/wiki/Opt_in
[3]: 04-Managing-content.md#balises-d-insertion
