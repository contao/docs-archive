# Data Container Arrays

Data Container Arrays (DCAs) are used to store table meta data. Each DCA
describes a particular table in terms of its configuration, its relations to
other tables and its fields. The Contao core engine determines by this meta data
how to list records, how to render back end forms and how to save data.  The DCA
files of all active module are loaded one after the other (starting with
"backend" and "frontend" and then in alphabetical order), so that every module
can override the existing configuration. The `system/config/dcaconfig.php` file
is included at the end.


## Reference

A Data Container Array is devided into six sections. The first section stores
the general table configuration like relations to other tables. The second and
third section determine how records are listed and which operations a user is
allowed to execute. The fourth section defines different groups of form fields
which are called "palettes" and the last two sections describe the input fields
in detail.


### Configuration de la table

La configuration de la table décrit la table elle-même, par exemple quel type de conteneur de données est utilisé pour stocker les données ou ses relations avec les autres tables. Vous pouvez également activer le versioning ou définir ce qui arrive aux enregistrements enfants lorsque les données sont éditées ou supprimées. 

<table>
<tr>
  <th>Clé</th>
  <th>Valeur</th>
  <th>Description</th>
</tr>
<tr>
  <td>label</td>
  <td><code>&amp;$GLOBALS['TL_LANG']</code> (<code>string</code>)</td>
  <td>Le libellé utilisé dans l'arborescence des pages ou des fichiers, et inclut typiquement une référence au tableau de langue.</td>
</tr>
<tr>
  <td>ptable</td>
  <td>Table parent (<code>string</code>)</td>
  <td>Le nom de la table parent (table.pid = ptable.id).</td>
</tr>
<tr>
  <td>ctable</td>
  <td>Tables enfants (<code>array</code>)</td>
  <td>Les noms des tables enfants (table.id = ctable.pid).</td>
</tr>
<tr>
  <td>dataContainer</td>
  <td>Conteneur de données (<code>string</code>)</td>
  <td>Table (table de la base de données), File (fichier de configuration local) ou Folder (gestionnaire de fichiers).</td>
</tr>
<tr>
  <td>validFileTypes</td>
  <td>Types de fichiers (<code>string</code>)</td>
  <td>Une liste d'extensions de fichiers valides, séparées par des virgules (ne s'applique qu'aux arborescences de fichiers).</td>
</tr>
<tr>
  <td>uploadScript</td>
  <td>Nom du fichier (<code>string</code>)</td>
  <td>Nom du script FancyUpload dans le répertoire system/config (sans l'extension de fichier).</td>
</tr>
<tr>
  <td>closed</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Si true, vous ne pouvez plus rajouter d'enregistrement dans cette table.</td>
</tr>
<tr>
  <td>notEditable</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Si true, la table ne peut pas être modifiée.</td>
</tr>
<tr>
  <td>notDeletable</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Si true, les enregistrements de la table ne peuvent pas être supprimés.</td>
</tr>
<tr>
  <td>switchToEdit</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Active le bouton « Sauvegarder et éditer » lorsqu'un nouvel enregistrement est ajouté (mode de tri 4 uniquement).</td>
</tr>
<tr>
  <td>enableVersioning</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Si true, Contao enregistre l'ancienne version de l'enregistrement lorsqu'une nouvelle version est créée.</td>
</tr>
<tr>
  <td>doNotCopyRecords</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Si true, Contao ne dupliquera pas les enregistrements de la table courante lorsqu'un enregistrement de sa table parente est dupliqué.</td>
</tr>
<tr>
  <td>doNotDeleteRecords</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Si true, Contao n'effacera pas les enregistrements de la table courante lorsqu'un enregistrement de sa table parente est effacé.</td>
</tr>
<tr>
  <td>onload_callback</td>
  <td>Fonction callback (<code>array</code>)</td>
  <td>Appelle une fonction personnalisée lorsqu'un DataContainer est initialisé, et passe l'objet DataContainer en argument.</td>
</tr>
<tr>
  <td>onsubmit_callback</td>
  <td>Fonction callback (<code>array</code>)</td>
  <td>Appelle une fonction personnalisée après la mise à jour d'un enregistrement, et passe l'objet DataContainer en argument.</td>
</tr>
<tr>
  <td>ondelete_callback</td>
  <td>Fonction callback (<code>array</code>)</td>
  <td>Appelle une fonction personnalisée après la suppression d'un enregistrement, et passe l'objet DataContainer en argument.</td>
</tr>
<tr>
  <td>oncut_callback</td>
  <td>Fonction callback (<code>array</code>)</td>
  <td>Appelle une fonction personnalisée lorsqu'un enregistrement est déplacé, et passe l'objet DataContainer en argument. Ajoutée à partir de la version 2.8.2 de Contao.</td>
</tr>
<tr>
  <td>oncopy_callback</td>
  <td>Fonction callback (<code>array</code>)</td>
  <td>Appelle une fonction personnalisée lorsqu'un enregistrement est dupliqué, et passe l'objet DataContainer en argument. Ajoutée à partir de la version 2.8.2 de Contao.</td>
</tr>
<tr>
  <td>sql</td>
  <td>Configuration de la table (<code>array</code>)</td>
  <td>Décrit la configuration de la table, par exemple
  <code>'keys' => array
  		(
				'id' => 'primary',
				'pid' => 'index'
			)</code></td>
</tr>
</table>


### Liste des enregistrements

Le tableau « listing » définit comment les enregistrements sont listés. Le moteur de Contao fournit trois [vues][1] différentes : la vue en liste, la vue parent et la vue arborescente. Vous pouvez configurer différentes options de tri, telles que des filtres ou un ordre de tri par défaut, et ajouter des libellés personnalisés. 


#### Tri

<table>
<tr>
  <th>Clé</th>
  <th>Valeur</th>
  <th>Description</th>
</tr>
<tr>
  <td>mode</td>
  <td>Mode de tri (<code>integer</code>)</td>
  <td><b>0</b> Les enregistrements ne sont pas triés<br>
      <b>1</b> Les enregistrements sont triés selon un champ déterminé<br>
      <b>2</b> Les enregistrements sont triés selon un champs sélectionnable<br>
      <b>3</b> Les enregistrements sont triés par la table parente<br>
      <b>4</b>Affiche les enregistrements enfants d'une table parente (voir le module feuilles de style)<br>
      <b>5</b> Les enregistrements sont présentés en arborescence (voir la structure du site)<br>
      <b>6</b> Affiche les enregistrements enfants dans une structure en arborescence (voir le module articles)</td>
</tr>
<tr>
  <td>flag</td>
  <td>Tri "flag" (<code>integer</code>)</td>
  <td><b>1</b> Tri ascendant sur la première lettre<br>
      <b>2</b> Tri descendant sur la première lettre<br>
      <b>3</b> Tri ascendant sur les deux premières lettres<br>
      <b>4</b> Tri descendant sur les deux premières lettres<br>
      <b>5</b> Tri ascendant par jour<br>
      <b>6</b> Tri descendant par jour<br>
      <b>7</b> Tri ascendant par mois<br>
      <b>8</b> Tri descendant par mois<br>
      <b>9</b> Tri ascendant par année<br>
      <b>10</b> Tri descendant par année<br>
      <b>11</b> Tri ascendant<br>
      <b>12</b> Tri descendant</td>
</tr>
<tr>
  <td>panelLayout</td>
  <td>Présentation du panneau (<code>string</code>)</td>
  <td><b>search</b> affiche le menu de recherche des enregistrements<br>
      <b>sort</b> affiche le menu de tri des enregistrements<br>
      <b>filter</b> affiche le menu de filtre des enregistrements<br>
      <b>limit</b> affiche le menu de limitation du nombre des enregistrements<br>
      <br>Les options doivent être séparées par des virgules (= espace) et des points virgules (= nouvelle ligne) comme <code>sort,filter;search,limit</code>.</td>
</tr>
<tr>
  <td>fields</td>
  <td>Valeurs de tri par défaut (<code>array</code>)</td>
  <td>Un ou plusieurs champs utilisés pour trier la table.</td>
</tr>
<tr>
  <td>headerFields</td>
  <td>Champs d'en-tête (<code>array</code>)</td>
  <td>Un ou plusieurs champs affichés dans l'élément en-tête (mode de tri 4 uniquement).</td>
</tr>
<tr>
  <td>icon</td>
  <td>Icône d'arborescence (<code>string</code>)</td>
  <td>Chemin de l'icône qui sera affichée au dessus de l'arborescence (mode de tri 5 et 6 uniquement).</td>
</tr>
<tr>
  <td>root</td>
  <td>Noeuds racines (<code>array</code>)</td>
  <td>ID des enregistrements racines (pagemounts). En général, cette valeur se gère toute seule.</td>
</tr>
<tr>
  <td>filter</td>
  <td>Filtre de requête (<code>array</code>)</td>
  <td>Vous permet d'ajouter des filtres personnalisés sous forme de tableaux, par exemple <code>array('status=?', 'active')</code>.</td>
</tr>
<tr>
  <td>disableGrouping</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Vous permet de désactiver les en-têtes de groupe dans les vues en liste et dans les vues parent. </td>
</tr>
<tr>
  <td>paste_button_callback</td>
  <td>Fonction callback (<code>array</code>)</td>
  <td>Cette fonction sera appelée au lieu d'afficher les boutons de collage par défaut. A spécifier en tant que <code>array('Class', 'Method')</code>.</td>
</tr>
<tr>
  <td>child_record_callback</td>
  <td>Fonction callback (<code>array</code>)</td>
  <td>Cette fonction sera appelée pour restituer les éléments enfants ( mode de tri 4 uniquement ). A spécifier en tant que <code>array('Class', 'Method')</code>.</td>
</tr>
<tr>
  <td>child_record_class</td>
  <td>Class CSS (<code>string</code>)</td>
  <td>Vous permet d'ajouter une classe CSS aux éléments de la vue parent.</td>
</tr>
</table>


#### Libellés

<table>
<tr>
  <th>Clé</th>
  <th>Valeur</th>
  <th>Description</th>
</tr>
<tr>
  <td>fields</td>
  <td>Champs (<code>array</code>)</td>
  <td>Un ou plusieurs champs qui seront affichés dans la liste.</td>
</tr>
<tr>
  <td>format</td>
  <td>Chaîne de formatage (<code>string</code>)</td>
  <td>Une chaîne de caractères HTML utilisée pour formater les champs qui seront affichés (par exemple <code><strong>%s</strong></code>).</td>
</tr>
<tr>
  <td>maxCharacters</td>
  <td>Nombre de caractères (<code>integer</code>)</td>
  <td>Nombre maximum de caractères du libellé.</td>
</tr>
<tr>
  <td>group_callback</td>
  <td>Fonction callback (<code>array</code>)</td>
  <td>Appelle une fonction personnalisée plutôt que la fonction par défaut pour l'entête de groupe.</td>
</tr>
<tr>
  <td>label_callback</td>
  <td>Fonction callback (<code>array</code>)</td>
  <td>Appelle une fonction personnalisée plutôt que la fonction libellé par défaut.</td>
</tr>
</table>


### Opérations

Le tableau des opérations est divisé en deux sections : les opérations globales, qui concernent tous les enregistrements à la fois (par exemple, modification de plusieurs enregistrements), et les opérations unitaires, qui concernent qu'un enregistrement spécifique (par exemple, modification ou suppression d'un enregistrement). 


#### Opérations globales

<table>
<tr>
  <th>Clé</th>
  <th>Valeur</th>
  <th>Description</th>
</tr>
<tr>
  <td>label</td>
  <td><code>&amp;$GLOBALS['TL_LANG']</code> (<code>string</code>)</td>
  <td>Label du bouton. Typiquement une référence au tableau global de langue.</td>
</tr>
<tr>
  <td>href</td>
  <td>Fragment d'URL (<code>string</code>)</td>
  <td>Un fragment d'URL ajouté au string d'URI lors du clic sur un bouton (par exemple, <code>act=editAll</code>).</td>
</tr>
<tr>
  <td>class</td>
  <td>Classe CSS (<code>string</code>)</td>
  <td>Attribut de classe CSS du bouton.</td>
</tr>
<tr>
  <td>attributes</td>
  <td>Attributs supplémentaires (<code>string</code>)</td>
  <td>Attributs supplémentaires, comme un gestionnaire d'événement ou des définitions de style.</td>
</tr>
<tr>
  <td>button_callback</td>
  <td>Callback function (<code>array</code>)</td>
  <td>Appelle une fonction personnalisée à la place de la fonction de bouton par défaut. A spécifier en tant que <code>array('Class', 'Method')</code>.</td>
</tr>
</table>


#### Opérations unitaires

<table>
<tr>
  <th>Clé</th>
  <th>Valeur</th>
  <th>Description</th>
</tr>
<tr>
  <td>label</td>
  <td><code>&amp;$GLOBALS['TL_LANG']</code> (<code>string</code>)</td>
  <td>Intitulé du bouton. Typiquement une référence au tableau global de langue. </td>
</tr>
<tr>
  <td>href</td>
  <td>Fragment d'URL (<code>string</code>)</td>
  <td>Fragment d'URL ajouté au string d'URI lors du clic sur le bouton (par exemple, <code>act=edit</code>). </td>
</tr>
<tr>
  <td>icon</td>
  <td>Icône (<code>string</code>)</td>
  <td>Chemin et nom de fichier de l'icône.</td>
</tr>
<tr>
  <td>attributes</td>
  <td>Attributs supplémentaires (<code>string</code>)</td>
  <td>Attributs supplémentaires comme un gestionnaire d'événement ou des définitions de style.</td>
</tr>
<tr>
  <td>button_callback</td>
  <td>Fonction callback (<code>array</code>)</td>
  <td>Appelle une fonction personnalisée à la place de la fonction de bouton par défaut. A spécifier en tant que <code>array('Class', 'Method')</code>.</td>
</tr>
</table>


### Champs

Le tableau des champs définit les colonnes d'une table. En fonction de ces paramétrages, le moteur de Contao détermine quel type de champs de formulaire à charger, si un utilisateur est autorisé ou non à accéder à certain champ, et si un champ peut être utilisé comme critère de tri ou de filtre. 

<table>
<tr>
  <th>Clé</th>
  <th>Valeur</th>
  <th>Description</th>
</tr>
<tr>
  <td>label</td>
  <td><code>&amp;$GLOBALS['TL_LANG']</code> (<code>string</code>)</td>
  <td>Intitulé du champ. Typiquement, une référence au tableau global de langue.</td>
</tr>
<tr>
  <td>default</td>
  <td>Valeur par défaut (<code>mixed</code>)</td>
  <td>Valeur par défaut attribuée quand un nouvel enregistrement est créé.</td>
</tr>
<tr>
  <td>exclude</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Si true, le champ sera exclu pour les non-administrateurs. Il peut être activé dans le module groupes d'utilisateurs (champs exclus acceptés).</td>
</tr>
<tr>
  <td>search</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Si true, le champ sera inclus dans le menu de recherche (voir "tri des enregistrements" -> "panelLayout").</td>
</tr>
<tr>
  <td>sorting</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Si true, le champ sera inclus dans le menu de tri (voir "tri des enregistrements" -> "panelLayout").</td>
</tr>
<tr>
  <td>filter</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Si true, le champ sera inclus dans le menu de filtrage (voir "tri des enregistrements" -> "panelLayout").</td>
</tr>
<tr>
  <td>flag</td>
  <td>Mode de tri (<code>integer</code>)</td>
  <td><b>1</b> Tri ascendant sur la première lettre<br>
      <b>2</b> Tri descendant sur la première lettre<br>
      <b>3</b> Tri ascendant sur les X premières lettres (voir length)<br>
      <b>4</b> Tri descendant sur les X premières lettres (voir length)<br>
      <b>5</b> Tri ascendant par jour<br>
      <b>6</b> Tri descendant par jour<br>
      <b>7</b> Tri ascendant par mois<br>
      <b>8</b> Tri descendant par mois<br>
      <b>9</b> Tri ascendant par année<br>
      <b>10</b> Tri descendant par année<br>
      <b>11</b> Tri ascendant<br>
      <b>12</b> Tri descendant</td>
</tr>
<tr>
  <td>length</td>
  <td>Longeur du critère de tri (<code>integer</code>)</td>
  <td>Permet de spécifier le nombre de caractères utilisés pour les groupes de tris (flags 3 et 4).</td>
</tr>
<tr>
  <td>inputType</td>
  <td>Type de champs (<code>string</code>)</td>
  <td><b>text</b> Champ texte<br>
      <b>password</b> Champ mot de passe<br>
      <b>textarea</b> Textarea<br>
      <b>select</b> Menu déroulant<br>
      <b>checkbox</b> Case à cocher<br>
      <b>radio</b> Bouton radio<br>
      <b>radioTable</b> Tableau avec images et boutons radio<br>
      <b>inputUnit</b> Champ texte avec petit menu déroulant d'éléments<br>
      <b>trbl</b> Quatre champs textes avec petit menu menu déroulant d'éléments<br>
      <b>chmod</b> Tableau CHMOD<br>
      <b>pageTree</b> Arborescence des pages<br>
      <b>fileTree</b> Arborescence des fichiers<br>
      <b>tableWizard</b> Assistant de tables<br>
      <b>listWizard</b> Assistant de listes<br>
      <b>optionWizard</b> Assistant d'options<br>
      <b>moduleWizard</b> Assistant de modules<br>
      <b>checkboxWizard</b> Assistant de cases à cocher</td>
</tr>
<tr>
  <td>options</td>
  <td>Options (<code>array</code>)</td>
  <td>Options d'un menu déroulant ou de boutons radio.</td>
</tr>
<tr>
  <td>options_callback</td>
  <td>Fonction callback (<code>array</code>)</td>
  <td>Fonction callback retournant un tableau d'options. A spécifier en tant que <code>array('Class', 'Method')</code>.</td>
</tr>
<tr>
  <td>foreignKey</td>
  <td>Table.champ (<code>string</code>)</td>
  <td>Récupère les options depuis une table de la base de données. Renvoie l'ID comme clé et le champ spécifié comme valeur.</td>
</tr>
<tr>
  <td>reference</td>
  <td><code>&amp;$GLOBALS['TL_LANG']</code> (<code>string</code>)</td>
  <td>Tableau contenant les intitulés des options. Typiquement, une référence au tableau global de langue.</td>
</tr>
<tr>
  <td>explanation</td>
  <td><code>&amp;$GLOBALS['TL_LANG']</code> (<code>string</code>)</td>
  <td>Tableau contenant les descriptions. Typiquement, une référence au tableau global de langue.</td>
</tr>
<tr>
  <td>input_field_callback</td>
  <td>Fonction callback (<code>array</code>)</td>
  <td>Exécute une fonction personnalisée à la saisie du champ, à la place de la routine par défaut, et passe l'objet DataContainer et le libellé en arguments.</td>
</tr>
<tr>
  <td>eval</td>
  <td>Configuration du champ (<code>array</code>)</td>
  <td>Diverses options de configuration. Voir le paragraphe suivant.</td>
</tr>
<tr>
  <td>wizard</td>
  <td>Fonction callback (<code>array</code>)</td>
  <td>Appelle une fonction et ajoute sa valeur de retour dans le champ de saisie. A spécifier en tant que <code>array('Class', 'Method')</code>.</td>
</tr>
<tr>
  <td>sql</td>
  <td>Définition d'un champ de base de données (<code>string</code>)</td>
  <td>Décrit le type de données et sa configuration de base de données, par exemple
      <code>varchar(255) NOT NULL default ''</code></td>
</tr>
<tr>
  <td>relation</td>
  <td>Configuration des relations (<code>array</code>)</td>
  <td>Décrit la relation à la table parent (voir le paragraphe "relations").
  </td>
</tr>
<tr>
  <td>load_callback</td>
  <td>Fonctions callback (<code>array</code>)</td>
  <td>Ces fonctions seront appelées au chargement du champ. Spécifiez chaque fonction de callback en tant que <code>array('Class', 'Method')</code>. Passe la valeur du champ et le conteneur de données en arguments. Attend la valeur du champ comme valeur de retour.</td>
</tr>
<tr>
  <td>save_callback</td>
  <td>Fonctions callback (<code>array</code>)</td>
  <td>Ces fonctions seront appelées à la sauvegarde du champ. Spécifiez chaque fonction de callback en tant que <code>array('Class', 'Method')</code>. Passe la valeur du champ et le conteneur de données en arguments. Attend la valeur du champ comme valeur de retour. Renvoie une exception pour afficher un message d'erreur.</td>
</tr>
</table>


### Évaluation

Le tableau d'évaluation configure en détail un champ particulier. Vous pouvez, par exemple, créer des champs obligatoires, ajouter un sélecteur de dates ou définir le nombre de lignes et de colonnes d'un bloc de texte (textarea). Vous pouvez aussi modifier l'apparence d'un champ ou activer l'encryptage des données. Chaque champ peut être validé par une expression régulière. 

<table>
<tr>
  <th>Clé</th>
  <th>Valeur</th>
  <th>Description</th>
</tr>
<tr>
  <td>helpwizard</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Si true, l'icône de l'assistant sera affichée à côté du libellé du champ.</td>
</tr>
<tr>
  <td>mandatory</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Si true, le champ ne peut pas être vide.</td>
</tr>
<tr>
  <td>maxlength</td>
  <td>Longueur maximale (<code>integer</code>)</td>
  <td>Nombre maximum de caractères autorisés dans le champ courant.</td>
</tr>
<tr>
  <td>minlength</td>
  <td>Longueur minimale (<code>integer</code>)</td>
  <td>Nombre minimum de caractères qui doivent être saisis.</td>
</tr>
<tr>
  <td>fallback</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>ISi true, le champ ne peut être assigné qu'une fois par table.</td>
</tr>
<tr>
    <td>rgxp</td>
  <td>Expression régulière (<code>string</code>)</td>
  <td>
    <table>
        <tr>
          <td><b>alias</b></td>
          <td>exige un alias valide</td>
        </tr>
        <tr>
          <td><b>alnum</b></td>
          <td>n'autorise que des caractères alphanumériques (y compris le point [.], 
          le trait d’union [-], le tiret bas [_] et l'espace [ ])</td>
        </tr>
        <tr>
          <td><b>alpha</b></td>
          <td>n'autorise que des caractères alphabétiques (y compris le point [.], 
          le trait d’union [-] et l'espace [ ])</td>
        </tr>
        <tr>
          <td><b>date</b></td>
          <td>exige une date valide</td>
        </tr>
        <tr>
          <td><b>datim</b></td>
          <td>exige une date et une heure valide</td>
        </tr>
        <tr>
          <td><b>digit</b></td>
          <td>n'autorise que des caractères numériques (y compris le point [.] et 
          le trait d’union [-])</td>
        </tr>
        <tr>
          <td><b>email</b></td>
          <td>exige une adresse e-mail valide </td>
        </tr>
        <tr>
          <td><b>emails</b></td>
          <td>exige une liste d'adresses e-mail valide</td>
        </tr>
        <tr>
          <td><b>extnd</b></td>
          <td>interdit <code>#&amp;()/&lt;=&gt;</code></td>
        </tr>
        <tr>
          <td><b>folderalias</b></td>
          <td>expects a valid folder URL alias</td>
        </tr>
        <tr>
          <td><b>friendly</b></td>
          <td>exige une adresse e-mail valide au format "nom convivial" (friendly name format)</td>
        </tr>
        <tr>
          <td><b>language</b></td>
          <td>exige un code de langue valide</td>
        </tr>
        <tr>
          <td><b>locale</b></td>
          <td>exige une "locale" valide (par exemple "fr-CH")</td>
        </tr>
        <tr>
          <td><b>phone</b></td>
          <td>exige un numéro de téléphone valide (caractères numériques, espace [ ], 
          plus [+], trait d’union [-], parenthèses [()] et barre oblique [/])</td>
        </tr>
        <tr>
          <td><b>prcnt</b></td>
          <td>autorise des nombres entre 0 et 100</td>
        </tr>
        <tr>
          <td><b>url</b></td>
          <td>exige une URL valide</td>
        </tr>
        <tr>
          <td><b>time</b></td>
          <td>exige une heure valide</td>
        </tr>
    </table>
  </td>
</tr>
<tr>
  <td>cols</td>
  <td>Colonnes (<code>integer</code>)</td>
  <td>Nombre de colonnes (champs textarea seulement).</td>
</tr>
<tr>
  <td>rows</td>
  <td>Lignes (<code>integer</code>)</td>
  <td>Nombre de lignes (champs textarea seulement).</td>
</tr>
<tr>
  <td>multiple</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Autorise les valeurs multiples. S'applique aux champs textes, listes déroulantes, boutons radios et cases à cocher. Requis pour l'assistant de cases à cocher.</td>
</tr>
<tr>
  <td>size</td>
  <td>Taille (<code>integer</code>)</td>
  <td>Taille d'une liste déroulante à choix multiples, ou nombre de champs de saisie.</td>
</tr>
<tr>
  <td>style</td>
  <td>Attributs de style (<code>string</code>)</td>
  <td>Attributs de style (par exemple <code>border:2px</code>)</td>
</tr>
<tr>
  <td>rte</td>
  <td>Éditeur de texte riche (<code>string</code>)</td>
  <td><b>tinyMCE</b> utilise le fichier <code>config/tinyMCE.php</code><br>
      <b>tinyFlash</b> utilise le fichier <code>config/tinyFlash.php</code><br>
      Vous pouvez également ajouter vos propres fichiers de configuration.</td>
</tr>
<tr>
  <td>submitOnChange</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Si true, le formulaire sera soumis lorsque la valeur du champ est modifiée.</td>
</tr>
<tr>
  <td>nospace</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Si true, les caractères d'espacement ne seront pas autorisés.</td>
</tr>
<tr>
  <td>allowHtml</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Si true, le champ courant acceptera le code HTML.</td>
</tr>
<tr>
  <td>preserveTags</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Si true, les balises HTML ne seront pas supprimées.</td>
</tr>
<tr>
  <td>decodeEntities</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Si true, les éléments HTML seront décodés. Notez que les éléments HTML sont toujours décodés si allowHtml vaut true.</td>
</tr>
<tr>
  <td>doNotSaveEmpty</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Si true, le champ ne sera pas enregistré s'il est vide.</td>
</tr>
<tr>
  <td>alwaysSave</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Si true, le champ sera toujours enregistré, même si sa valeur n'a pas changé. Cela peut être utile en conjonction d'un load_callback.</td>
</tr>
<tr>
  <td>spaceToUnderscore</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Si true, tous les caractères d'espacement seront remplacés par un tiret bas.</td>
</tr>
<tr>
  <td>unique</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Si true, la valeur du champ ne peut être enregistrée si elle existe déjà.</td>
</tr>
<tr>
  <td>encrypt</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Si true, la valeur du champ sera stockée sous forme cryptée.</td>
</tr>
<tr>
  <td>trailingSlash</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Si true, une barre oblique sera ajoutée à la fin de la valeur du champ. Si false, la barre oblique, si existante, qui termine la valeur du champ sera supprimée.</td>
</tr>
<tr>
  <td>files</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Si true, les fichiers et les dossiers seront affichés. Si false, seuls les dossiers seront affichés. Ne s'applique qu'aux arborescences de fichiers.</td>
</tr>
<tr>
  <td>filesOnly</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Supprime les boutons radio ou les cases à cocher à côté des noms de dossiers. Ne s'applique qu'aux arborescences de fichiers.</td>
</tr>
<tr>
  <td>extensions</td>
  <td>Extensions de fichiers (<code>string</code>)</td>
  <td>N'autorise que certaines extensions dans l'arborescence de fichiers (liste séparée par des virgules). Ne s'applique qu'aux arborescences de fichiers.</td>
</tr>
<tr>
  <td>path</td>
  <td>Chemin (<code>string</code>)</td>
  <td>Dossier racine personnalisé pour l'arborescence de fichiers. Ne s'applique qu'aux arborescences de fichiers.</td>
</tr>
<tr>
  <td>fieldType</td>
  <td>Type de champ d'entrée (<code>string</code>)</td>
  <td><b>checkbox</b> autorise les sélections multiples<br>
      <b>radio</b> n'autorise qu'une seule sélection<br>
      Ne s'applique qu'aux arborescences de fichiers et de pages.</td>
</tr>
<tr>
  <td>includeBlankOption</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Si true, une option vide sera ajoutée au tableau des options. Ne s'applique qu'aux listes déroulantes.</td>
</tr>
<tr>
  <td>blankOptionLabel</td>
  <td>Libellé (<code>string</code>)</td>
  <td>Libellé pour l'option vide (par défaut <code>-</code>).</td>
</tr>
<tr>
  <td>chosen</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Balises "select" natives améliorées avec
      <a href="http://harvesthq.github.io/chosen/" target="_blank">Chosen</a>.</td>
</tr>
<tr>
  <td>findInSet</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Tri sur les valeurs actuelles des options plutôt que sur leurs libellés.</td>
</tr>
<tr>
  <td>datepicker</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Si true, le champ actuel a un sélecteur de dates.</td>
</tr>
<tr>
  <td>colorpicker</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Si true, le champ actuel a un sélecteur de couleurs</td>
</tr>
<tr>
  <td>feEditable</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Si true, le champ courant peut être modifié dans le front office. Ne s'applique qu'à la table <code>tl_member</code>.</td>
</tr>
<tr>
  <td>feGroup</td>
  <td>Group name (<code>string</code>)</td>
  <td><b>personal</b> données personnelles<br>
      <b>address</b> détails de l'adresse<br>
      <b>contact</b> détails de contact<br>
      <b>login</b> détails d'identification (uniquement la table <code>tl_member</code>)<br>
      Vous pouvez également définir vos propres groupes.</td>
</tr>
<tr>
  <td>feViewable</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Si true, le champ courant est affiché dans le module de listes des membres.</td>
</tr>
<tr>
  <td>doNotCopy</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Si true, le champ courant ne sera pas dupliqué lorsque l'enregistrement est dupliqué.</td>
</tr>
<tr>
  <td>hideInput</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Si true, la valeur du champ sera cachée (elle sera cependant visible dans la source de la page !).</td>
</tr>
<tr>
  <td>doNotShow</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Si true, le champ courant ne sera pas affiché dans les modes "modifier tous" et "voir les détails".</td>
</tr>
<tr>
  <td>isBoolean</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Indique qu'un champ particulier est de type booléen.</td>
</tr>
<tr>
  <td>disabled</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Désactive le champ (n'est pas supporté par tous les types de champs).</td>
</tr>
<tr>
  <td>readonly</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Rend le champ en lecture seule (n'est pas supporté par tous les types de champs).</td>
</tr>
</table>


### Relations

Relations describes, how database fields are related to other tables. 
Define the referenced table in the `foreignKey` key. Relations provide 
model classes to load referenced data sets efficiently and developer friendly.
(see `Model::getRelated()`).

<table>
<tr>
  <th>Clé</th>
  <th>Valeur</th>
  <th>Description</th>
</tr>
<tr>
  <td>type</td>
  <td>Type of relation<br> (<code>string</code>)
  <td>
    <b>hasOne</b> Value references a child data set<br>
    <b>hasMany</b> Value references some child data sets
       (serialized)<br>
    <b>belongsTo</b> Value references a parent data set
       (z.B. <code>pid</code>)<br>
    <b>belongsToMany</b> Value references some parent data sets
       (serialized)<br>
  </td>
</tr>
<tr>
  <td>load</td>
  <td>Load behaviour<br> (<code>string</code>)</td>
  <td>
      <b>lazy</b> Loading referenced records only when necessary
         (default, saves RAM)<br>
      <b>eager</b> Loading referenced records automatically (saves database calls)
  </td>
</tr>
</table>


## Palettes

A palette is a group of form fields which are required to edit a record. A
palette typically does not include all columns of a table but only the ones that
belong to a particular module or content element. Palettes can change
dynamically depending on the user's permissions or type of element and certain
subparts of the form (called subpalettes) can be loaded interactively via Ajax.


### Defining groups

A palette is a string of field names which are concatenated with either a
semicolon (;) or a comma (,). Whereas the comma is just used to separate the
field names, the semicolon indicates the beginning of a new fieldset, which can
be expanded and collapsed.

![](https://raw.github.com/contao/docs/3.1/manual/en/images/palettes.jpg)

The above example is defined by the following code:

``` {.php}
{title_legend},headline,alias,author;{date_legend},date,time;{teaser_legend:hide},subheadline,teaser
```

The `title_legend` and `date_legend` placeholders will be replaced with the
corresponding labels from the "TL_LANG" array.

``` {.php}
$GLOBALS['TL_LANG']['tl_news']['title_legend'] = 'Title and author';
$GLOBALS['TL_LANG']['tl_news']['date_legend']  = 'Date and time';
```


### Arranging fields

The Contao back end uses a simple two-column grid system to arrange input fields
within their groups. You can apply the following CSS classes in the evaluation
section of the Data Container Array as `tl_class` (e.g. `'tl_class'=>'w50
wizard'`).

<table>
<tr>
  <th>tl_class</th>
  <th>Description</th>
</tr>
<tr>
  <td>w50</td>
  <td>Set the field width to 50% and float it (<code>float:left</code>).</td>
</tr>
<tr>
  <td>clr</td>
  <td>Clear all floats.</td>
</tr>
<tr>
  <td>wizard</td>
  <td>Shorten the input field so there is enough room for the wizard button
      (e.g. date picker fields).</td>
</tr>
<tr>
  <td>long</td>
  <td>Make the text input field span two columns.</td>
</tr>
<tr>
  <td>m12</td>
  <td>Add a 12 pixel top margin to the element (used for single
      checkboxes).</td>
</tr>
</table>


## Callbacks

Callback functions are based on the event dispatcher pattern. You can register
one or more callbacks for a certain event and when the event is triggered, the
callback functions are being executed. Callbacks allow you to customize the
program flow of the Contao core engine.


#### Global callbacks

<table>
<tr>
  <th>Callback</th>
  <th>Description</th>
</tr>
<tr>
  <td>onload_callback</td>
  <td>Is executed when the DataContainer object is initialized. Allows you to
      e.g. check permissions or to modify the Data Container Array dynamically
      at runtime.</td>
</tr>
<tr>
  <td>onsubmit_callback</td>
  <td>Is executed when a back end form is submitted. Allows you to e.g. modify
      the form data before it is written to the database (used to calculate
      intervals in the calendar extension).</td>
</tr>
<tr>
  <td>ondelete_callback</td>
  <td>Is executed before a record is removed from the database.</td>
</tr>
<tr>
  <td>oncut_callback</td>
  <td>Is executed after a record has been moved to a new position.</td>
</tr>
<tr>
  <td>oncopy_callback</td>
  <td>Is executed after a record has been duplicated.</td>
</tr>
</table>


#### Listing callbacks

<table>
<tr>
  <th>Callback</th>
  <th>Description</th>
</tr>
<tr>
  <td>paste_button_callback</td>
  <td>Allows for individual paste buttons and is e.g. used in the site structure
      to disable buttons depending on the user's permissions (requires an
      additional command check via load_callback).</td>
</tr>
<tr>
  <td>child_record_callback</td>
  <td>Defines how child elements are rendered in "parent view".</td>
</tr>
<tr>
  <td>group_callback</td>
  <td>Allows for individual group headers in the listing.</td>
</tr>
<tr>
  <td>label_callback</td>
  <td>Allows for individual labels in the listing and is e.g. used in the user
      module to add status icons.</td>
</tr>
</table>


#### Operations callbacks

<table>
<tr>
  <th>Callback</th>
  <th>Description</th>
</tr>
<tr>
  <td>button_callback</td>
  <td>Allows for individual navigation icons and is e.g. used in the site
      structure to disable buttons depending on the user's permissions (requires
      an additional command check via load_callback).</td>
</tr>
</table>


#### Field callbacks

<table>
<tr>
  <th>Callback</th>
  <th>Description</th>
</tr>
<tr>
  <td>options_callback</td>
  <td>Allows you to define an individual function to load data into a drop-down
      menu or checkbox list. Useful e.g. for conditional
      foreinKey-relations.</td>
</tr>
<tr>
  <td>input_field_callback</td>
  <td>Allows for the creation of individual form fields and is e.g. used in the
      back end module "personal data" to generate the "purge data" widget.
      Attention: the field is not saved automatically!</td>
</tr>
<tr>
  <td>load_callback</td>
  <td>Is executed when a form field is initialized and can e.g. be used to load
      a default value.</td>
</tr>
<tr>
  <td>save_callback</td>
  <td>Is executed when a field is submitted and can e.g. be used to add an
      individual validation routine.</td>
</tr>
</table>


[1]: 02-Administration-area.md#listing-records
