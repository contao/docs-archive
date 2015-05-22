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


### Module front office

Le module front office est utilisé pour afficher des formulaires sur le
site internet. Il peut être configuré avec le module "Modules" dans le
back office et doit être ajouté à un article ou à une présentation de
page pour pouvoir apparaître sur le site internet. L'extension générateur
de formulaire comprend un module front office :

<table>
<tr>
  <th>Module</th>
  <th>Classe CSS</th>
  <th>Description</th>
</tr>
<tr>
  <td>Formulaire</td>
  <td>mod_form</td>
  <td>Ajoute un formulaire dans la page.</td>
</tr>
</table>


### Élément de contenu

L'élément de contenu est utilisé pour afficher des formulaires sur le site
internet. Il peut être configuré avec l'élément de contenu "Formulaire"
dans le back office et doit être ajouté à un article pour pouvoir apparaître
sur le site internet. L'extension générateur de formulaire comprend un élément
de contenu :

<table>
<tr>
  <th>Élément de contenu</th>
  <th>Classe CSS</th>
  <th>Description</th>
</tr>
<tr>
  <td>Formulaire</td>
  <td>ce_form</td>
  <td>Insère un formulaire.</td>
</tr>
</table>
