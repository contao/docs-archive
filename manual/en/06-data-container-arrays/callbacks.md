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
