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

![](images/element-protege.jpg?raw=true)


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
