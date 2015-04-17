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
http://www.example.com/news/items/james-wilson-returns.html
```

L'URL ci-dessus sollicite l'actualité "james-Wilson-retours" via la page 
"actualités". Rappelez-vous que Contao est un CMS basé sur les pages, donc si 
la page "actualités" n'existait pas ou si elle ne comprenait pas le module 
lecteur d'actualités, alors l'actualité ne serait pas affichée.
