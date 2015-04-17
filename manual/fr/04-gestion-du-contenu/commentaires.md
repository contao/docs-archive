## Commentaires

Les commentaires sont une autre forme de contenu que vous pouvez gérer à partir
du back office. Les commentaires doivent être activés dans les préférences des
calendriers et des archives d'actualités.


### Module front office

Le module front office est utilisé pour afficher des commentaires sur le 
site internet. Il peut être configuré avec le module "Modules" dans le 
back office et doit être ajouté à un article ou à une présentation de 
page pour pouvoir apparaître sur le site internet. L'extension commentaires 
comprend un module front office :

<table>
<tr>
  <th>Module</th>
  <th>Classe CSS</th>
  <th>Description</th>
</tr>
<tr>
  <td>Commentaires</td>
  <td>mod_comments</td>
  <td>Gérer les commentaires ou les entrées d'un livre d'or.</td>
</tr>
</table>


### Élément de contenu

L'élément de contenu est utilisé pour afficher des commentaires sur le site 
internet. Il peut être configuré avec l'élément de contenu "Commentaires"
dans le back office et doit être ajouté à un article pour pouvoir apparaître 
sur le site internet. L'extension commentaires comprend un élément de contenu :

<table>
<tr>
  <th>Élément de contenu</th>
  <th>Classe CSS</th>
  <th>Description</th>
</tr>
<tr>
  <td>Commentaires</td>
  <td>ce_comments</td>
  <td>Ajouter un formulaire de saisie de commentaires à la page.</td>
</tr>
</table>


### BBCode

Vous pouvez permettre aux utilisateurs du front office d'utiliser
le [langage de balisage BBCode][7].

Contao prend en charge les balises suivantes :

<table>
<tr>
  <th>BBCode</th>
  <th>Définition</th>
</tr>
<tr>
  <td>[b][/b]</td>
  <td>Remplace la balise avec un texte en gras.</td>
</tr>
<tr>
  <td>[i][/i]</td>
  <td>Remplace la balise avec un texte en italique.</td>
</tr>
<tr>
  <td>[u][/u]</td>
  <td>Remplace la balise avec un texte souligné.</td>
</tr>
<tr>
  <td>[img][/img]</td>
  <td>Remplace la balise avec une image (Ajouter une URL entre les balises).</td>
</tr>
<tr>
  <td>[code][/code]</td>
  <td>Remplace la balise avec un texte à espacement fixe.</td>
</tr>
<tr>
  <td>[color=#ff0000][/color]</td>
  <td>Remplace la balise avec un texte en couleur.</td>
</tr>
<tr>
  <td>[quote][/quote]</td>
  <td>Remplace la balise avec un texte cité.</td>
</tr>
<tr>
  <td>[quote=John]Bonjour[/quote]</td>
  <td>Remplace la balise avec un texte cité et le nom de l'auteur (par exemple,
  John a écrit: Bonjour).</td>
</tr>
<tr>
  <td>[url][/url]</td>
  <td>Remplace la balise avec un lien.</td>
</tr>
<tr>
  <td>[url=http://][/url]</td>
  <td>Remplace la balise avec un lien (insérer l'URL en tant que paramètre)</td>
</tr>
<tr>
  <td>[email][/email]</td>
  <td>Remplace la balise avec un lien mailto.</td>
</tr>
<tr>
  <td>[email=name@example.com][/email]</td>
  <td>Remplace la balise avec un lien mailto (insérer l'adresse e-mail en tant
  que paramètre).</td>
</tr>
</table>


[7]: http://fr.wikipedia.org/wiki/Bbcode