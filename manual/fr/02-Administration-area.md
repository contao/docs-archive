# Panneau d'administration

Pour accéder au panneau d'administration de Contao (back office), ajouter 
simplement `/contao` à l'URL de votre site internet. Le formulaire 
d'identification du back office est protégé contre les attaques par force brute, 
donc si vous entrez un mot de passe erroné plus de trois fois de suite, votre 
compte sera bloqué durant 5 minutes.


## Liste d'enregistrements

Contao supporte trois vues: une simple liste ("vue en liste"), une liste qui est 
regroupée par sa table parente («vue parente») et une liste hiérarchique ("vue 
arborescente"). Ces trois vues peuvent être utilisées pour lister des 
enregistrements de n'importe quelle table ou de tables liées entre elles.


### Vue en liste

La "vue en liste" répertorie les enregistrements d'une table unique dans un 
ordre particulier. Les résultats sont généralement regroupés par leur première 
lettre.

![](https://raw.github.com/contao/docs/3.1/manual/fr/images/vue-liste.jpg)


### Vue parente

La "vue parente" répertorie les enregistrements d'une table enfant qui sont liés 
à un enregistrement particulier d'une table parente. Les relations de type 
parent-enfant sont beaucoup utilisées dans Contao. Par exemple, pour les 
articles et les éléments de contenu, les archives d'actualités et les actualités 
ou les feuilles de style et les définitions de formatage.

![](https://raw.github.com/contao/docs/3.1/manual/fr/images/vue-parente.jpg)


### Vue arborescente

La "vue arborescente" liste des enregistrements et d'autres ressources tels 
que des fichiers et des répertoires qui sont organisés dans une structure 
hiérarchique. Contao prend en charge les relations hiérarchiques au sein d'une 
table (par exemple, la structure de site) ainsi que des tables enfants qui se 
rapportent aux tables hiérarchiques parentes (par exemple, les articles et les 
pages).

![](https://raw.github.com/contao/docs/3.1/manual/fr/images/vue-arborescente.jpg)


### Tri et filtrage des données

Contao supporte différentes façons d'affiner les résultats de sorte que vous ne 
lâchiez pas le fil même si une table possède plusieurs milliers de lignes. Un 
grand nombre d'entrées peuvent être filtrées par un ou plusieurs champs de sorte 
qu'ils ne montrent que les enregistrements correspondant aux critères de 
filtrage. La plupart des entrées offrent de plus une recherche en texte intégral 
qui prend même en charge les expressions régulières. Afin de réduire le temps de 
chargement de la page au minimum, Contao affiche seulement trente 
enregistrements à la fois.

![](https://raw.github.com/contao/docs/3.1/manual/fr/images/trier-et-filtrer.jpg)


## Édition des enregistrements

L'édition des données est l'une des fonctions centrales d'un système de gestion 
de contenu. Contao offre beaucoup de fonctionnalités professionnelles qui 
rendent le processus d'édition aussi facile et confortable que possible. Vous 
pouvez revenir à des versions antérieures d'un enregistrement, restaurer des 
enregistrements supprimés, déplacer des enregistrements via le presse-papiers et 
même éditer plusieurs enregistrements à la fois. La plupart de ces fonctions 
sont accessibles en utilisant les icônes de navigation.


### Icônes de la vue en liste

La "vue en liste", étant la plus simple, ne propose que quatre actions de base : 
éditer, dupliquer, supprimer et afficher les détails.

![](https://raw.github.com/contao/docs/3.1/manual/fr/images/vue-liste-icones.jpg)


### Icônes de la vue parente

La "vue parente" propose deux icônes de navigation supplémentaires pour contrôler 
l'ordre des enregistrements. L'ordre peut être modifié par glisser-déposer. Pour 
ce faire, cliquez simplement sur l'icône de navigation "Glisser-déposer" et 
faites-le glisser vers sa nouvelle position.

![](https://raw.github.com/contao/docs/3.1/manual/fr/images/vue-parente-icones.jpg)


### Icônes de la vue arborescente

La "vue arborescente" nécessite des icônes supplémentaires pour gérer la 
structure hiérarchique. Outre la duplication d'un enregistrement unique, il 
prend en charge la duplication d'un enregistrement avec tous ses 
sous-enregistrements ainsi que la fonction "coller après" ou "coller dedans" un 
autre enregistrement, vous pouvez donc créer une structure imbriquée.

![](https://raw.github.com/contao/docs/3.1/manual/fr/images/vue-arborescente-icones.jpg)


### Restaurer les versions précédentes

Contao crée automatiquement les nouvelles versions d'un enregistrement chaque 
fois que vous le sauvegarder. Dès qu'il existe plus d'une version, un menu 
déroulant, qui vous permet de revenir à une version antérieure, apparaît en haut 
du formulaire. Choisissez simplement une version et cliquez sur le bouton 
"Restaurer".

L'icône située à droite du bouton "Restaurer" vous permet de voir les 
différences entre deux versions.

![](https://raw.github.com/contao/docs/3.1/manual/fr/images/version.jpg)


### Édition de plusieurs enregistrements

La possibilité de modifier plusieurs enregistrements à la fois permet à Contao 
de clairement se démarquer de la variété des systèmes de gestion de contenu. 
Cliquez sur le bouton "Édition multiple" afin de changer le mode d'édition, puis 
sélectionnez un ou plusieurs enregistrements et choisissez les champs que vous 
souhaitez modifier.

![](https://raw.github.com/contao/docs/3.1/manual/fr/images/selectionner-multiple-enregistrements.jpg)

![](https://raw.github.com/contao/docs/3.1/manual/fr/images/selectionner-champs-a-editer.jpg)

![](https://raw.github.com/contao/docs/3.1/manual/fr/images/editer-multiple-enregistrements.jpg)


## Raccourcis clavier

Afin d'accélérer le flux de travail lorsque vous travaillez avec Contao, il 
existe plusieurs raccourcis associés au back office qui vous permettent 
d'exécuter certaines commandes. Vous pouvez par exemple déclencher le bouton 
"Enregistrer" à la fin d'un formulaire en cliquant avec votre souris ou en 
utilisant le raccourci clavier `[Alt]+[s]`.


### Raccourcis clavier généraux

<table>
<tr>
  <th>Raccourci</th>
  <th>Bouton</th>
  <th>Explication</th>
</tr>
<tr>
  <td><code>[Alt]+[h]</code></td>
  <td>Accueil</td>
  <td>Aller à la page d'accueil du back office.</td>
</tr>
<tr>
  <td><code>[Alt]+[q]</code></td>
  <td><b>Q</b>uitter</td>
  <td>Quitter la session en cours du back office (Déconnexion).</td>
</tr>
<tr>
  <td><code>[Alt]+[t]</code></td>
  <td>Haut de la page</td>
  <td>Aller en haut de la page.</td>
</tr>
<tr>
  <td><code>[Alt]+[b]</code></td>
  <td>Retour</td>
  <td>Retour à la page précédente.</td>
</tr>
<tr>
  <td><code>[Alt]+[n]</code></td>
  <td><b>N</b>ouvel enregistrement</td>
  <td>Créer un nouvel enregistrement.</td>
</tr>
<tr>
  <td><code>[Alt]+[e]</code></td>
  <td>Édition multiple</td>
  <td>Passe en mode d'édition multiple.</td>
</tr>
<tr>
  <td><code>[Alt]+[f]</code></td>
  <td>Aperçu du <b>F</b>ront office</td>
  <td>Ouvrir l'aperçu du front office dans une nouvelle fenêtre du navigateur.
  </td>
</tr>
</table>


### Raccourcis clavier en mode d'édition

<table>
<tr>
  <th>Raccourci</th>
  <th>Bouton</th>
  <th>Explication</th>
</tr>
<tr>
  <td><code>[Alt]+[s]</code></td>
  <td><b>S</b>auvegarder</td>
  <td>Sauvegarde le formulaire courant</td>
</tr>
<tr>
  <td><code>[Alt]+[c]</code></td>
  <td>Sauvegarder et fermer</td>
  <td>Sauvegarde le formulaire courant et redirige vers la page précédente.
  </td>
</tr>
<tr>
  <td><code>[Alt]+[g]</code></td>
  <td>Sauvegarder et retour</td>
  <td>Sauvegarde le formulaire courant et redirige vers la page parente, par 
  exemple, à partir d'un élément de contenu vers la vue arborescente des 
  articles.</td>
</tr>
<tr>
  <td><code>[Alt]+[e]</code></td>
  <td>Sauvegarder et éditer</td>
  <td>Sauvegarde le formulaire courant et redirige vers la vue des 
  enregistrements enfants. Par exemple, lors de la création de feuilles de 
  style.</td>
</tr>
<tr>
  <td><code>[Alt]+[n]</code></td>
  <td>Sauvegarder et <b>n</b>ouveau</td>
  <td>Sauvegarde le formulaire courant et crée un nouvel enregistrement.</td>
</tr>
</table>


### Raccourcis clavier en mode d'édition multiple

<table>
<tr>
  <th>Raccourci</th>
  <th>Bouton</th>
  <th>Explication</th>
</tr>
<tr>
  <td><code>[Alt]+[d]</code></td>
  <td>Suppression multiple</td>
  <td>Supprime tous les enregistrements sélectionnés en mode d'édition 
  multiple.</td>
</tr>
<tr>
  <td><code>[Alt]+[x]</code></td>
  <td>Coupe multiple</td>
  <td>Déplace tous les enregistrements sélectionnés en mode d'édition 
  multiple.</td>
</tr>
<tr>
  <td><code>[Alt]+[c]</code></td>
  <td><b>C</b>opie multiple</td>
  <td>Duplique tous les enregistrements sélectionnés en mode d'édition 
  multiple.</td>
</tr>
<tr>
  <td><code>[Alt]+[v]</code></td>
  <td>Remplacement multiple</td>
  <td>Remplace tous les enregistrements sélectionnés en mode d'édition 
  multiple.</td>
</tr>
</table>

Les raccourcis clavier ci-dessus ne fonctionnent que sous Windows sous cette 
forme. Les utilisateurs de Mac doivent utiliser `[Ctrl]+[⌥ Opt]` au lieu de la 
touche `[Alt]` avec le raccourci clavier. En outre, Firefox sur Windows fait 
exception à la norme : vous devez appuyer sur le raccourci clavier 
`[Alt]+[Shift]`.
