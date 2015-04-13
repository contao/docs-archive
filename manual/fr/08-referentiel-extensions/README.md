# Référentiel d'extensions

Pour publier votre propre extension dans le référentiel d'extensions, vous avez 
besoin d'un [compte de contributeur][1]. Une fois que vous êtes connecté, vous 
pouvez accéder à l'interface du développeur du [référentiel d'extensions][2] 
par l'intermédiaire des liens "Manage extensions" et "Manage translations".


## Ajout d'une extension

Pour ajouter une nouvelle extension, suivez le lien "Manage extensions" et 
cliquez sur le bouton "Add extension". Vous serez redirigé vers un formulaire 
où vous pouvez entrer les détails de l'extension. La boîte jaune au-dessus 
contient des informations importantes sur les conventions de nommage, que 
vous devriez lire attentivement.

![](../en/images/add-extension.jpg?raw=true)

Les catégories suivantes sont actuellement disponibles :

<table>
<tr>
  <th>Catégorie</th>
  <th>Description</th>
</tr>
<tr>
  <td>Application</td>
  <td>L'extension est une application autonome.</td>
</tr>
<tr>
  <td>Plugin</td>
  <td>L'extension est une librairie PHP ou JavaScript.</td>
</tr>
<tr>
  <td>Theme</td>
  <td>L'extension est un thème pour le back office.</td>
</tr>
<tr>
  <td>Utility</td>
  <td>L'extension est un programme utilitaire pour le back office.</td>
</tr>
<tr>
  <td>Widget</td>
  <td>L'extension est un widget de formulaire.</td>
</tr>
<tr>
  <td>Translation</td>
  <td>L'extension est une traduction d'une version de Contao.</td>
</tr>
<tr>
  <td>Bundle</td>
  <td>Un ensemble d'extensions qui peuvent être installées simultanément.</td>
</tr>
<tr>
  <td>Other</td>
  <td>L'extension n'entre dans aucune des catégories précédentes.</td>
</tr>
</table>


## Ajouter une release

Après avoir créé une extension, vous pouvez ajouter une première release. 
Chaque nouvelle version d'une extension sera enregistrée comme une release 
séparée. Ouvrez les gestionnaire de releases grâce à l'icône de navigation 
correspondante et cliquez sur le bouton "Add release".

![](../en/images/add-release.jpg?raw=true)

Les numéros de versions dans le référentiel d'extensions sont formés de trois 
blocs de chiffres qui indiquent s'il s'agit d'une version majeure, mineure ou 
de maintenance (par exemple `1.0.0`) ainsi qu'un statut de développement sous 
forme de texte (par exemple `beta1`).

<table>
<tr>
  <th>Status</th>
  <th>Description</th>
</tr>
<tr>
  <td>alpha1 - alpha3</td>
  <td>Indique qu'il s'agit d'une version alpha.</td>
</tr>
<tr>
  <td>beta1 - beta3</td>
  <td>Indique qu'il s'agit d'une version bêta.</td>
</tr>
<tr>
  <td>rc1 - rc3</td>
  <td>Indique qu'il s'agit d'une version release candidate.</td>
</tr>
<tr>
  <td>stable</td>
  <td>Indique qu'il s'agit d'une version stable pour des systèmes en 
  production.</td>
</tr>
</table>


## Ajouter des fichiers

Vous devez ensuite ajouter des fichiers à la nouvelle release. Ouvrez le 
gestionnaire de fichiers, et cliquez sur le bouton "Add/update files". Vous 
pouvez téléverser des fichiers individuellement ou des archives .zip complètes. 
Assurez-vous de choisir le bon répertoire cible, afin que les chemins d'accès 
soient corrects à l'issue de l'envoi.

![](../en/images/add-files.jpg?raw=true)

![](../en/images/edit-files.jpg?raw=true)


## Ajout de fichiers à partir d'un référentiel GitHub

Les fichiers peuvent également être importés à partir d'un référentiel GitHub, 
si vous avez tagué la release et poussé le tag vers le référentiel central de 
GitHub.

Entrez l'URL HTTPS du référentiel GitHub dans les paramètres.

Vous pouvez également spécifier le nom du répertoire racine de votre référentiel. 
Dans ce cas, les fichiers et les répertoires en dehors de ce répertoire racine 
seront ignorés lors de l'importation.

![](../en/images/github-import.jpg?raw=true)

Si vous sélectionnez un tag, ses fichiers seront téléchargés automatiquement 
et seront alors disponibles comme lors d'un téléversement manuel.

![](../en/images/github-import-tag.jpg?raw=true)


## Ajouter des traductions

Avant de pouvoir publier une extension, vous devez créer au moins une 
traduction. Ouvrez le gestionnaire de traductions et cliquez sur le bouton 
"Add language". Il est recommandé de toujours créer une traduction anglaise, 
car les utilisateurs de back office ne voient généralement, dans le gestionnaire 
d'extensions, que les extensions disponibles dans leur propre langue ou en 
anglais (langue par défaut).

![](../en/images/add-translation.jpg?raw=true)

![](../en/images/edit-translation.jpg?raw=true)

Les traductions complétées peuvent être publiées en cliquant sur l'icône de 
navigation correspondante.


## Ajouter des dépendances

Peut-être que l'une de vos extensions utilise les fonctionalités d'une autre 
extension comme par exemple les tâches planifiées (cron jobs). Pour faire 
fonctionner votre extension, l'installation de l'extension cron constitue donc 
un pré-requis, généralement appelé dépendance. Ces dépendances peuvent être 
enregistrées dans le référentiel d'extensions, de telle sorte que les modules 
nécessaires soient automatiquement installés lorsque vous installez une 
extension particulière.

![](../en/images/add-dependency.jpg?raw=true)

Choisissez d'abord l'extension que vous souhaitez ajouter en tant que dépendance 
et confirmez votre choix en cliquant sur le bouton "Continue". Puis sélectionnez 
la version minimale et maximale dont le fonctionnement avec votre extension est 
reconnu.


## Publier une extension

Après avoir créé au minimum une release, téléversé au minimum un fichier, publié 
au minimum une traduction et ajouté les dépendances nécessaires, vous pouvez 
publier l'extension grâce à l'icône de navigation correspondante. Notez que vous 
ne pouvez plus supprimer l'extension une fois qu'elle est publiée. Pour vérifier 
si tout fonctionne comme prévu, connectez-vous dans le back office et faites un 
test d'installation avec le gestionnaire d'extensions.


[1]: https://contao.org/en/register.html
[2]: https://contao.org/en/extension-list.html
