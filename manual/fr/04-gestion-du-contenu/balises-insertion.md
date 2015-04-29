## Balises d'insertion

Les balises d'insertion sont des jokers qui sont remplacés par du contenu 
dynamique quand une page est affichée à l'écran. Elles vous permettent, par 
exemple, d'afficher la date courante, l'adresse d'un membre en fonction de 
son nom ou bien d'inclure un fichier. Les balises d'insertion peuvent être 
utilisées presque partout dans Contao, même dans les pages en cache.


### Les éléments de lien

Les balises d'insertion suivantes vous permettent de faire un lien vers une 
autre page ou vers un article en utilisant son ID ou son alias.

{% raw %}
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
  <td>Cette balise sera remplacée par un lien qui pointe vers la dernière page
  visitée. Elle peut aussi être utilisée comme <code>{{link_open::back}}</code>,
  <code>{{link_url::back}}</code> ou <code>{{link_title::back}}</code>
  (voir ci-dessous).</td>
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
{% endraw %}


### Propriétés de l'utilisateur

Les balises d'insertion suivantes vous permettent d'afficher n'importe quelle 
propriété du membre actuellement connecté. 

{% raw %}
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
{% endraw %}


### Propriétés de page

Les balises d'insertion suivantes vous permettent d'afficher n'importe quelle 
propriété de la page courante. 

{% raw %}
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
  <td>Cette balise sera remplacée par le nom du site internet.</td>
</tr>
<tr>
  <td><code>{{page::rootPageTitle}}</code></td>
  <td>Cette balise sera remplacée par le titre du site internet.</td>
</tr>
</table>
{% endraw %}


### Variables d'environnement

Les balises d'insertion suivantes vous permettent d'afficher les variables 
d'environnement comme le nom de la page ou la chaîne de requête. 

{% raw %}
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
  <td><code>{{env::assets_url}}</code></td>
  <td>Cette balise sera remplacée par l'URL statique du répertoire assets.
  </td>
</tr>
</table>
{% endraw %}


### Éléments inclus

Les balises d'insertion suivantes vous permettent d'inclure différentes 
ressources comme des articles, des modules ou des fichiers qui se trouvent dans 
le répertoire "templates". 

{% raw %}
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
  <td><code>{{insert_form::*}}</code></td>
  <td>Cette balise sera remplacée par le formulaire référencé (remplacez * par 
  l'ID du formulaire).</td>
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
  Vous pouvez également récupérer le chemin d'un fichier à partir de la base de
  données avec son UUID :
  <code>{{file::6939a448-9b30-11e4-bcba-079af1e9baea}}</code>.</td>
</tr>
</table>
{% endraw %}


### Divers

Les balises d'insertion suivantes vous permettent d'effectuer différentes 
tâches comme ajouter la date courante ou ajouter des images lightbox.

{% raw %}
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
  <code>{{ifnlng::de}}Your name{{ifnlng}}{{iflng::de}}Ihr Name{{iflng}}</code>.
  </td>
</tr>
<tr>
  <td><code>{{image::*}}</code></td>
  <td>Cette balise sera remplacée par une vignette d'image (remplacer * 
  avec l'ID de base de données, UUID ou un chemin de fichier système) :
      <code>{{image::58ca4a90-2d30-11e4-8c21-0800200c9a66?width=200&amp;height=150}}</code>.
      <br /><strong>width</strong>: Largeur de la vignette,<br />
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
  <td><code>{{version}}</code></td>
  <td>Cette balise sera remplacée par la version actuelle de Contao (par exemple 
  2.11.2).</td>
</tr>
<tr>
  <td><code>{{request_token}}</code></td>
  <td>Cette balise sera remplacée par la demande de jeton de la session en cours.
  </td>
</tr>
<tr>
  <td><code>{{toggle_view}}</code></td>
  <td>Ajoute le lien qui vous permet de basculer entre le modèle pour mobile et 
  celui d'un ordinateur de bureau.</td>
</tr>
</table>
{% endraw %}


### Drapeaux des balises d'insertion

En utilisant des drapeaux, les balises d'insertion peuvent être traitées de 
manière plus approfondie. Par exemple, la valeur peut être transmise aux 
méthodes PHP spécifiques. Plusieurs drapeaux peuvent être appliqués :

```
{{ua::browser|uncached}}  
{{page::title|decodeEntities|strtoupper}}
```

Drapeaux disponibles :

{% raw %}
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
    <td>Identique à <code>nl2br</code>, mais conserve les retours à la ligne
    dans la balise <code>&lt;pre&gt;</code></td>
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
    <td>Voir <code>String::encodeEmail</code></td>
</tr>
<tr>
    <td><code>decodeEntities</code></td>
    <td>Décode les entités de caractère HTML dans la sortie</td>
    <td>Voir <code>String::decodeEntities()</code></td>
</tr>
<tr>
    <td><code>number_format</code></td>
    <td>Formate un numéro (sans décimale)</td>
    <td>Voir <code>System::getFormattedNumber()</code></td>
</tr>
<tr>
    <td><code>currency_format</code></td>
    <td>Formate une devise (deux décimales)</td>
    <td>Voir <code>System::getFormattedNumber()</code></td>
</tr>
<tr>
    <td><code>readable_size</code></td>
    <td>Convertit des tailles de fichiers dans un format lisible par 
    un humain</td>
    <td>Voir <code>System::getReadableSize()</code></td>
</tr>
</table>
{% endraw %}
