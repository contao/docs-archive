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

Les modules front office sont utilisés pour afficher des événements sur le 
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
http://www.example.com/event-reader/events/final-exams.html
```

L'URL ci-dessus sollicite l'événement "final-exams" via la page "events". 
Rappelez-vous que Contao est un CMS basé sur les pages, donc si la page "events" 
n'existait pas ou si elle n'incluait pas le module lecteur d'événements, alors
l'événement ne serait pas affiché. 
