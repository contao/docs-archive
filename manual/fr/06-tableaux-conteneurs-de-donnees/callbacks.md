## Callbacks

Les fonctions callback sont fondées sur un pattern de répartition d'événements.
Vous pouvez inscrire une ou plusieurs callbacks pour un certain événement et
lorsque l'événement est déclenché, les fonctions callback sont exécutées. Les
callbacks vous permettent de personnaliser le cours de l'exécution du cœur
de Contao.


### Callbacks globaux

<table>
<tr>
  <th>Callback</th>
  <th>Description</th>
</tr>
<tr>
  <td>onload_callback</td>
  <td>Est exécutée quand l'objet DataContainer est initialisé. Cela vous permet,
  par exemple, de vérifier les permissions ou de modifier le tableau conteneur
  de données dynamiquement à l'exécution.</td>
</tr>
<tr>
  <td>onsubmit_callback</td>
  <td>Est exécutée lorsqu'un formulaire du back office est soumis. Cela vous
  permet, par exemple, de modifier les données du formulaire avant qu'elles ne
  soient écrites dans la base de données (utilisée pour calculer les intervalles
  dans l'extension calendrier).</td>
</tr>
<tr>
  <td>ondelete_callback</td>
  <td>Est exécutée avant qu'un enregistrement soit supprimé de la base de
  données.</td>
</tr>
<tr>
  <td>oncut_callback</td>
  <td>Est exécutée après qu'un enregistrement ait été déplacé vers une nouvelle
  position.</td>
</tr>
<tr>
  <td>oncopy_callback</td>
  <td>Est exécutée après qu'un enregistrement ait été dupliqué.</td>
</tr>
</table>


### Callbacks de listing

<table>
<tr>
  <th>Callback</th>
  <th>Description</th>
</tr>
<tr>
  <td>paste_button_callback</td>
  <td>Permet d'avoir des boutons de collage individuels et est, par exemple,
  utilisée dans la structure de site pour désactiver les boutons en fonction
  des permissions de l'utilisateur (nécessite un contrôle de commande
  additionnel via load_callback).</td>
</tr>
<tr>
  <td>child_record_callback</td>
  <td>Définit comment les éléments enfants sont rendus dans la "vue parente".
  </td>
</tr>
<tr>
  <td>group_callback</td>
  <td>Permet d'avoir des en-têtes de groupes individuels dans le listing.
  </td>
</tr>
<tr>
  <td>label_callback</td>
  <td>Permet d'avoir des libellés individuels dans le listing et est, par
  exemple, utilisée dans le module utilisateurs pour ajouter des icônes de
  statut.</td>
</tr>
</table>


### Callbacks d'opérations

<table>
<tr>
  <th>Callback</th>
  <th>Description</th>
</tr>
<tr>
  <td>button_callback</td>
  <td>Permet d'avoir des icônes de navigation individuels et est, par exemple,
  utilisée dans la structure de site pour désactiver des boutons en fonction
  des permissions de l'utilisateur (nécessite un contrôle de commande
  additionnel via load_callback).</td>
</tr>
</table>


### Callbacks de champs

<table>
<tr>
  <th>Callback</th>
  <th>Description</th>
</tr>
<tr>
  <td>options_callback</td>
  <td>Vous permet de définir une fonction individuelle pour charger des données
  dans un menu déroulant ou une liste de cases à cocher. Utile, par exemple,
  pour des relations avec clés étrangères conditionnelles.</td>
</tr>
<tr>
  <td>input_field_callback</td>
  <td>Permet la création de champs de formulaire individuels et est, par
  exemple, utilisée dans le module back office "données personnelles" pour
  générer le widget "nettoyer les données". Attention : le champs n'est pas
  sauvegardé automatiquement !</td>
</tr>
<tr>
  <td>load_callback</td>
  <td>Est exécutée lorsque un champs de formulaire est initialisé et peut, par
  exemple, être utilisée pour charger une valeur par défaut.</td>
</tr>
<tr>
  <td>save_callback</td>
  <td>Est exécutée quand un champs est soumis et peut, par exemple, être
  utilisée pour ajouter une routine de validation individuelle.</td>
</tr>
</table>
