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


### Table configuration

The table configuration describes the table itself, e.g. which type of data
container is used to store the data or how it relates to other tables. Also you
can enable versioning or define what happens to child records when data is being
edited or deleted.

<table>
<tr>
  <th>Key</th>
  <th>Value</th>
  <th>Description</th>
</tr>
<tr>
  <td>label</td>
  <td>`&$GLOBALS['TL_LANG']` (`string`)</td>
  <td>The label is used with page or file trees and typically includes reference
      to the language array.</td>
</tr>
<tr>
  <td>ptable</td>
  <td>Parent table (`string`)</td>
  <td>Name of the related parent table (table.pid = ptable.id).</td>
</tr>
<tr>
  <td>ctable</td>
  <td>Child tables (`array`)</td>
  <td>Name of the related child tables (table.id = ctable.pid).</td>
</tr>
<tr>
  <td>dataContainer</td>
  <td>Data Container (`string`)</td>
  <td>Table (database table), File (local configuration file) or Folder (file
      manager).</td>
</tr>
<tr>
  <td>validFileTypes</td>
  <td>File types (`string`)</td>
  <td>Comma separated list of valid file extensions (applies to file trees
      only).</td>
</tr>
<tr>
  <td>uploadScript</td>
  <td>File name (`string`)</td>
  <td>Name of the FancyUpload script in the system/config folder (without file
      extension).</td>
</tr>
<tr>
  <td>closed</td>
  <td>true/false (`boolean`)</td>
  <td>If true, you cannot add further records to the table.</td>
</tr>
<tr>
  <td>notEditable</td>
  <td>true/false (`boolean`)</td>
  <td>If true, the table cannot be edited.</td>
</tr>
<tr>
  <td>switchToEdit</td>
  <td>true/false (`boolean`)</td>
  <td>Activates the "save and edit" button when a new record is added (sorting
      mode 4 only).</td>
</tr>
<tr>
  <td>enableVersioning</td>
  <td>true/false (`boolean`)</td>
  <td>If true, Contao saves the old version of a record when a new version is
      created.</td>
</tr>
<tr>
  <td>doNotCopyRecords</td>
  <td>true/false (`boolean`)</td>
  <td>If true, Contao will not duplicate records of the current table when a
      record of its parent table is duplicated.</td>
</tr>
<tr>
  <td>doNotDeleteRecords</td>
  <td>true/false (`boolean`)</td>
  <td>If true, Contao will not delete records of the current table when a record
      of its parent table is deleted.</td>
</tr>
<tr>
  <td>onload_callback</td>
  <td>Callback function (`array`)</td>
  <td>Calls a custom function when a DataContainer is initialized and passes the
      DataContainer object as argument.</td>
</tr>
<tr>
  <td>onsubmit_callback</td>
  <td>Callback function (`array`)</td>
  <td>Calls a custom function after a record has been updated and passes the
      DataContainer object as argument.</td>
</tr>
<tr>
  <td>ondelete_callback</td>
  <td>Callback function (`array`)</td>
  <td>Calls a custom function when a record is deleted and passes the
      DataContainer object as argument.</td>
</tr>
<tr>
  <td>oncut_callback</td>
  <td>Callback function (`array`)</td>
  <td>Calls a custom function when a record is moved and passes the
      DataContainer object as argument. Added in version 2.8.2.</td>
</tr>
<tr>
  <td>oncopy_callback</td>
  <td>Callback function (`array`)</td>
  <td>Calls a custom function when a record is duplicated and passes the insert
      ID and the DataContainer object as argument. Added in version 2.8.2.</td>
</tr>
</table>


### Listing records

The listing array defines how records are listed. The Contao core engine
supports three different [views][1]: "list view", "parent view" and "tree view".
You can configure various sorting options like filters or the default sorting
order and you can add custom labels.


#### Sorting

<table>
<tr>
  <th>Key</th>
  <th>Value</th>
  <th>Description</th>
</tr>
<tr>
  <td>mode</td>
  <td>Sorting mode (`integer`)</td>
  <td>**0** Records are not sorted, **1** Records are sorted by a fixed field,
      **2** Records are sorted by a switchable field, **3** Records are sorted
      by the parent table, **4** Displays the child records of a parent record
      (see style sheets module), **5** Records are displayed as tree (see site
      structure), **6** Displays the child records within a tree structure (see
      articles module)</td>
</tr>
<tr>
  <td>flag</td>
  <td>Sorting flag (`integer`)</td>
  <td>**1** Sort by initial letter ascending, **2** Sort by initial letter
      descending, **3** Sort by initial two letters ascending, **4** Sort by
      initial two letters descending, **5** Sort by day ascending, **6** Sort by
      day descending, **7** Sort by month ascending, **8** Sort by month
      descending, **9** Sort by year ascending, **10** Sort by year descending,
      **11** Sort ascending, **12** Sort descending</td>
</tr>
<tr>
  <td>panelLayout</td>
  <td>Panel layout (`string`)</td>
  <td>**search** show the search records menu, **sort** show the sort records
      menu, **filter** show the filter records menu, **limit** show the limit
      records menu. Separate options with comma (= space) and semicolon (= new
      line) like `sort,filter;search,limit`.</td>
</tr>
<tr>
  <td>fields</td>
  <td>Default sorting values (`array`)</td>
  <td>One or more fields that are used to sort the table.</td>
</tr>
<tr>
  <td>headerFields</td>
  <td>Header fields (`array`)</td>
  <td>One or more fields that will be shown in the header element (sorting mode
      4 only).</td>
</tr>
<tr>
  <td>icon</td>
  <td>Tree icon (`string`)</td>
  <td>Path to an icon that will be shown on top of the tree (sorting mode 5 and
      6 only).</td>
</tr>
<tr>
  <td>root</td>
  <td>Root nodes (`array`)</td>
  <td>IDs of the root records (pagemounts). This value usually takes care of
      itself.</td>
</tr>
<tr>
  <td>filter</td>
  <td>Query filter (`array`)</td>
  <td>Allows you to add custom filters as arrays, e.g. `array('status=?',
      'active')`.</td>
</tr>
<tr>
  <td>disableGrouping</td>
  <td>true/false (`boolean`)</td>
  <td>Allows you to disable the group headers in list view and parent view.</td>
</tr>
<tr>
  <td>paste_button_callback</td>
  <td>Callback function (`array`)</td>
  <td>This function will be called instead of displaying the default paste
      buttons. Please specify as `array('Class', 'Method')`.</td>
</tr>
<tr>
  <td>child_record_callback</td>
  <td>Callback function (`array`)</td>
  <td>This function will be called to render the child elements (sorting mode 4
      only). Please specify as `array('Class', 'Method')`.</td>
</tr>
<tr>
  <td>child_record_class</td>
  <td>CSS class (`string`)</td>
  <td>Allows you to add a CSS class to the parent view elements.</td>
</tr>
</table>


#### Labels

<table>
<tr>
  <th>Key</th>
  <th>Value</th>
  <th>Description</th>
</tr>
<tr>
  <td>fields</td>
  <td>Fields (`array`)</td>
  <td>One or more fields that will be shown in the list.</td>
</tr>
<tr>
  <td>format</td>
  <td>Format string (`string`)</td>
  <td>HTML string used to format the fields that will be shown (e.g.
      `<strong>%s</strong>`).</td>
</tr>
<tr>
  <td>maxCharacters</td>
  <td>Number of characters (`integer`)</td>
  <td>Maximum number of characters of the label.</td>
</tr>
<tr>
  <td>group_callback</td>
  <td>Callback function (`array`)</td>
  <td>Call a custom function instead of using the default group header
      function.</td>
</tr>
<tr>
  <td>label_callback</td>
  <td>Callback function (`array`)</td>
  <td>Call a custom function instead of using the default label function.</td>
</tr>
</table>


### Operations

The operations array is divided into two sections: global operations that relate
to all records at once (e.g. editing multiple records) and regular operations
that relate to a particular record only (e.g. editing or deleting a record).


#### Global operations

<table>
<tr>
  <th>Key</th>
  <th>Value</th>
  <th>Description</th>
</tr>
<tr>
  <td>label</td>
  <td>`&$GLOBALS['TL_LANG']` (`string`)</td>
  <td>Button label. Typically a reference to the global language array.</td>
</tr>
<tr>
  <td>href</td>
  <td>URL fragment (`string`)</td>
  <td>URL fragment that is added to the URI string when the button is clicked
      (e.g. `act=editAll`).</td>
</tr>
<tr>
  <td>class</td>
  <td>CSS class (`string`)</td>
  <td>CSS class attribute of the button.</td>
</tr>
<tr>
  <td>attributes</td>
  <td>Additional attributes (`string`)</td>
  <td>Additional attributes like event handler or style definitions.</td>
</tr>
<tr>
  <td>button_callback</td>
  <td>Callback function (`array`)</td>
  <td>Call a custom function instead of using the default button function.
      Please specify as `array('Class', 'Method')`.</td>
</tr>
</table>


#### Regular operations

<table>
<tr>
  <th>Key</th>
  <th>Value</th>
  <th>Description</th>
</tr>
<tr>
  <td>label</td>
  <td>`&$GLOBALS['TL_LANG']` (`string`)</td>
  <td>Button label. Typically a reference to the global language array.</td>
</tr>
<tr>
  <td>href</td>
  <td>URL fragment (`string`)</td>
  <td>URL fragment that is added to the URI string when the button is clicked
      (e.g. `act=edit`).</td>
</tr>
<tr>
  <td>icon</td>
  <td>Icon (`string`)</td>
  <td>Path and filename of the icon.</td>
</tr>
<tr>
  <td>attributes</td>
  <td>Additional attributes (`string`)</td>
  <td>Additional attributes like event handler or style definitions.</td>
</tr>
<tr>
  <td>button_callback</td>
  <td>Callback function (`array`)</td>
  <td>Call a custom function instead of using the default button function.
      Please specify as `array('Class', 'Method')`.</td>
</tr>
</table>


### Fields

The fields array defines the columns of a table. Depending on these settings,
the Contao core engine decides which type of form field to load, whether a user
is allowed to access a certain field and whether a field can be used as sort or
filter criteria.

<table>
<tr>
  <th>Key</th>
  <th>Value</th>
  <th>Description</th>
</tr>
<tr>
  <td>label</td>
  <td>`&$GLOBALS['TL_LANG']` (`string`)</td>
  <td>Field label. Typically a reference to the global language array.</td>
</tr>
<tr>
  <td>default</td>
  <td>Default value<br />"mixed"</td>
  <td>Default value that is set when a new record is created.</td>
</tr>
<tr>
  <td>exclude</td>
  <td>true/false (`boolean`)</td>
  <td>If true the field will be excluded for non-admins. It can be enabled in
      the user group module (allowed excluded fields).</td>
</tr>
<tr>
  <td>search</td>
  <td>true/false (`boolean`)</td>
  <td>If true the field will be included in the search menu (see "sorting
      records" -> "panelLayout").</td>
</tr>
<tr>
  <td>sorting</td>
  <td>true/false (`boolean`)</td>
  <td>If true the field will be included in the sorting menu (see "sorting
      records" -> "panelLayout").</td>
</tr>
<tr>
  <td>filter</td>
  <td>true/false (`boolean`)</td>
  <td>If true the field will be included in the filter menu (see "sorting
      records" -> "panelLayout").</td>
</tr>
<tr>
  <td>flag</td>
  <td>Sorting mode (`integer`)</td>
  <td>**1** Sort by initial letter ascending, **2** Sort by initial letter
      descending, **3** Sort by initial X letters ascending (see length), **4**
      Sort by initial X letters descending (see length), **5** Sort by day
      ascending, **6** Sort by day descending, **7** Sort by month ascending,
      **8** Sort by month descending, **9** Sort by year ascending, **10** Sort
      by year descending, **11** Sort ascending, **12** Sort descending</td>
</tr>
<tr>
  <td>length</td>
  <td>Sorting length (`integer`)</td>
  <td>Allows to specify the number of characters that are used to build sorting
      groups (flag 3 and 4).</td>
</tr>
<tr>
  <td>inputType</td>
  <td>Field type (`string`)</td>
  <td>**text** Text field, **password** Password field, **textarea** Textarea,
      **select** Drop-down menu, **checkbox** Checkbox, **radio** Radio button,
      **radioTable** Table with images and radio buttons, **inputUnit** Text
      field with small unit drop-down menu, **trbl** Four text fields with a
      small unit drop-down menu, **chmod** CHMOD table, **pageTree** Page tree,
      **fileTree** File tree, **tableWizard** Table wizard, **listWizard** List
      wizard, **optionWizard** Option wizard, **moduleWizard** Module wizard,
      **checkboxWizard** Checkbox Wizard</td>
</tr>
<tr>
  <td>options</td>
  <td>Options (`array`)</td>
  <td>Options of a drop-down menu or radio button menu.</td>
</tr>
<tr>
  <td>options_callback</td>
  <td>Callback function (`array`)</td>
  <td>Callback function that returns an array of options. Please specify as
      `array('Class', 'Method')`.</td>
</tr>
<tr>
  <td>foreignKey</td>
  <td>table.field (`string`)</td>
  <td>Get options from a database table. Returns ID as key and the field you
      specify as value.</td>
</tr>
<tr>
  <td>reference</td>
  <td>`&$GLOBALS['TL_LANG']` (`string`)</td>
  <td>Array that holds the options labels. Typically a reference to the global
      language array.</td>
</tr>
<tr>
  <td>explanation</td>
  <td>`&$GLOBALS['TL_LANG']` (`string`)</td>
  <td>Array that holds the explanation. Typically a reference to the global
      language array.</td>
</tr>
<tr>
  <td>input_field_callback</td>
  <td>Callback function (`array`)</td>
  <td>Executes a custom function instead of using the default input field
      routine and passes the the DataContainer object and the label as
      arguments.</td>
</tr>
<tr>
  <td>eval</td>
  <td>Field configuration (`array`)</td>
  <td>Various configuration options. See next paragraph.</td>
</tr>
<tr>
  <td>wizard</td>
  <td>Callback function (`array`)</td>
  <td>Call a custom function and add its return value to the input field. Please
      specify as `array('Class', 'Method')`.</td>
</tr>
<tr>
  <td>load_callback</td>
  <td>Callback functions (`array`)</td>
  <td>These functions will be called when the field is loaded. Please specify
      each callback function as `array('Class', 'Method')`. Passes the field's
      value and the data container as arguments. Expects the field value as
      return value.</td>
</tr>
<tr>
  <td>save_callback</td>
  <td>Callback functions (`array`)</td>
  <td>These functions will be called when the field is saved. Please specify
      each callback function as array('Class', 'Method'). Passes the field's
      value and the data container as arguments. Expects the field value as
      return value. Throw an exception to display an error message.</td>
</tr>
</table>


### Evaluation

The evaluation array configures a particular field in detail. You can e.g.
create mandatory fields, add a date picker or define the rows and columns of a
textarea. You can also modify the field appearance or enable data encryption.
Each field can be validated against a regular expression.

<table>
<tr>
  <th>Key</th>
  <th>Value</th>
  <th>Description</th>
</tr>
<tr>
  <td>helpwizard</td>
  <td>true/false (`boolean`)</td>
  <td>If true the helpwizard icon will appear next to the field label.</td>
</tr>
<tr>
  <td>mandatory</td>
  <td>true/false (`boolean`)</td>
  <td>If true the field cannot be empty.</td>
</tr>
<tr>
  <td>maxlength</td>
  <td>Maximum length (`integer`)</td>
  <td>Maximum number of characters that is allowed in the current field.</td>
</tr>
<tr>
  <td>minlength</td>
  <td>Minimum length (`integer`)</td>
  <td>Minimum number of characters that have to be entered.</td>
</tr>
<tr>
  <td>fallback</td>
  <td>true/false (`boolean`)</td>
  <td>If true the field can only be assigned once per table.</td>
</tr>
<tr>
  <td>rgxp</td>
  <td>Regular expression (`string`)</td>
  <td>**digit** allows numeric characters only, **alpha** allows alphabetic
      characters only, **alnum** allows alphanumeric characters only, **prcnt**
      allows numbers between 0 and 100, **extnd** disallows `#&amp;()/<=>`,
      **date** expects a valid date, **time** expects avalid time, **datim**
      expects a valid date and time, **email** expects a valid e-mail address,
      **friendly** expects a valid "friendly name format" e-mail address,
      **url** expects a valid URL, **phone** expects a valid phone number</td>
</tr>
<tr>
  <td>cols</td>
  <td>Columns (`integer`)</td>
  <td>Number of columns (textarea fields only).</td>
</tr>
<tr>
  <td>rows</td>
  <td>Rows (`integer`)</td>
  <td>Number of rows (textarea fields only).</td>
</tr>
<tr>
  <td>wrap</td>
  <td>Word wrapping (`string`)</td>
  <td>**off** disable word wrapping, **soft** soft word wrapping, **hard** hard
      word wrapping</td>
</tr>
<tr>
  <td>multiple</td>
  <td>true/false (`boolean`)</td>
  <td>Make the input field multiple. Applies to text fields, select menus, radio
      buttons and checkboxes. Required for the checkbox wizard.</td>
</tr>
<tr>
  <td>size</td>
  <td>Size (`integer`)</td>
  <td>Size of a multiple select menu or number of input fields.</td>
</tr>
<tr>
  <td>style</td>
  <td>Style attributes (`string`)</td>
  <td>Style attributes (e.g. border:2px)</td>
</tr>
<tr>
  <td>rte</td>
  <td>Rich text editor file (`string`)</td>
  <td>**tinyMCE** use file config/tinyMCE.php, **tinyFlash** use file
      `config/tinyFlash.php`. You can add your own configuration files too.</td>
</tr>
<tr>
  <td>submitOnChange</td>
  <td>true/false (`boolean`)</td>
  <td>If true the form will be submitted when the field value changes.</td>
</tr>
<tr>
  <td>nospace</td>
  <td>true/false (`boolean`)</td>
  <td>If true whitespace characters will not be allowed.</td>
</tr>
<tr>
  <td>allowHtml</td>
  <td>true/false (`boolean`)</td>
  <td>If true the current field will accept HTML input.</td>
</tr>
<tr>
  <td>preserveTags</td>
  <td>true/false (`boolean`)</td>
  <td>If true no HTML tags will be removed at all.</td>
</tr>
<tr>
  <td>decodeEntities</td>
  <td>true/false (`boolean`)</td>
  <td>If true HTML entities will be decoded. Note that HTML entities are always
      decoded if allowHtml is true.</td>
</tr>
<tr>
  <td>doNotSaveEmpty</td>
  <td>true/false (`boolean`)</td>
  <td>If true the field will not be saved if it is empty.</td>
</tr>
<tr>
  <td>alwaysSave</td>
  <td>true/false (`boolean`)</td>
  <td>If true the field will always be saved, even if its value has not changed.
      This can be useful in conjunction with a load_callback.</td>
</tr>
<tr>
  <td>spaceToUnderscore</td>
  <td>true/false (`boolean`)</td>
  <td>If true any whitespace character will be replaced by an underscore.</td>
</tr>
<tr>
  <td>unique</td>
  <td>true/false (`boolean`)</td>
  <td>If true the field value cannot be saved if it exists already.</td>
</tr>
<tr>
  <td>encrypt</td>
  <td>true/false (`boolean`)</td>
  <td>If true the field value will be stored encrypted.</td>
</tr>
<tr>
  <td>trailingSlash</td>
  <td>true/false (`boolean`)</td>
  <td>If true a trailing slash will be added to the field value. If false, an
      existing trailing slash will be removed from the field value.</td>
</tr>
<tr>
  <td>files</td>
  <td>true/false (`boolean`)</td>
  <td>If true files and folders will be shown. If false, only folders will be
      shown. Applies to file trees only.</td>
</tr>
<tr>
  <td>filesOnly</td>
  <td>true/false (`boolean`)</td>
  <td>Removes the radio buttons or checkboxes next to folders. Applies to file
      trees only.</td>
</tr>
<tr>
  <td>extensions</td>
  <td>File extensions (`string`)</td>
  <td>Limits the file tree to certain filetypes (comma separated list). Applies
      to file trees only.</td>
</tr>
<tr>
  <td>path</td>
  <td>Path (`string`)</td>
  <td>Custom root directory for file trees. Applies to file trees only.</td>
</tr>
<tr>
  <td>fieldType</td>
  <td>Input field type (`string`)</td>
  <td>**checkbox** allow multiple selections, **radio** allow a single selection
      only. Applies to file- and pagetrees only.</td>
</tr>
<tr>
  <td>includeBlankOption</td>
  <td>true/false (`boolean`)</td>
  <td>If true a blank option will be added to the options array. Applies to
      drop-down menus only.</td>
</tr>
<tr>
  <td>blankOptionLabel</td>
  <td>Label (`string`)</td>
  <td>Label for the blank option (defaults to -).</td>
</tr>
<tr>
  <td>findInSet</td>
  <td>true/false (`boolean`)</td>
  <td>Sort by the actual option values instead of their labels (available from
      version 2.7.RC1).</td>
</tr>
<tr>
  <td>datepicker</td>
  <td>Date picker (`string`)</td>
  <td>Date picker configuration string.</td>
</tr>
<tr>
  <td>feEditable</td>
  <td>true/false (`boolean`)</td>
  <td>If true the current field can be edited in the frontend. Applies to table
      tl_member only.</td>
</tr>
<tr>
  <td>feGroup</td>
  <td>Group name (`string`)</td>
  <td>**personal** personal data, **address** address details, **contact**
      contact details, **login** login details. Applies to table `tl_member`
      only. You can also define your own groups.</td>
</tr>
<tr>
  <td>feViewable</td>
  <td>true/false (`boolean`)</td>
  <td>If true the current field is viewable in the member listing module.</td>
</tr>
<tr>
  <td>doNotCopy</td>
  <td>true/false (`boolean`)</td>
  <td>If true the current field will not be duplicated if the record is
      duplicated.</td>
</tr>
<tr>
  <td>hideInput</td>
  <td>true/false (`boolean`)</td>
  <td>If true the field value will be hidden (it is still visible in the page
      source though!).</td>
</tr>
<tr>
  <td>doNotShow</td>
  <td>true/false (`boolean`)</td>
  <td>If true the current field will not be shown in "edit all" or "show
      details" mode.</td>
</tr>
<tr>
  <td>isBoolean</td>
  <td>true/false (`boolean`)</td>
  <td>Indicates that a particular field is boolean.</td>
</tr>
<tr>
  <td>disabled</td>
  <td>true/false (`boolean`)</td>
  <td>Disables the field (not supported by all field types).</td>
</tr>
<tr>
  <td>readonly</td>
  <td>true/false (`boolean`)</td>
  <td>Makes the field read only (not supported by all field types).</td>
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

![](images/palettes.jpg)

The above example is defined by the following code:

``` {.php}
{title_legend},headline,alias,author;{date_legend},date,time;{teaser_legend:hide},subheadline,teaser
```

The "title_legend" and "date_legend" placeholders will be replaced with the
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
  <td>Set the field width to 50% and float it (`float:left`).</td>
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


[1]: https://contao.org/en/listing-records.html
