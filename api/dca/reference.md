## Reference

A Data Container Array is divided into six sections. The first section stores
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

| Key                | Value                             | Description                                                                                                                                     |
|--------------------|-----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|
| label              | `&$GLOBALS['TL_LANG']` (`string`) | The label is used with page or file trees and typically includes reference to the language array.                                               |
| ptable             | Parent table (`string`)           | Name of the related parent table (table.pid = ptable.id).                                                                                       |
| ctable             | Child tables (`array`)            | Name of the related child tables (table.id = ctable.pid).                                                                                       |
| dataContainer      | Data Container (`string`)         | Table (database table), File (local configuration file) or Folder (file manager).                                                               |
| closed             | true/false (`boolean`)            | If true, you cannot add further records to the table.                                                                                           |
| notEditable        | true/false (`boolean`)            | If true, the table cannot be edited.                                                                                                            |
| notDeletable       | true/false (`boolean`)            | If true, records in the table cannot be deleted.                                                                                                |
| notSortable        | true/false (`boolean`)            | If true, records in the table cannot be sorted.                                                                                                 |
| notCopyable        | true/false (`boolean`)            | If true, records in the table cannot be duplicated.                                                                                             |
| notCreatable       | true/false (`boolean`)            | If true, records in the table cannot be created but can be duplicated.                                                                          |
| switchToEdit       | true/false (`boolean`)            | Activates the "save and edit" button when a new record is added (sorting mode 4 only).                                                          |
| enableVersioning   | true/false (`boolean`)            | If true, Contao saves the old version of a record when a new version is created.                                                                |
| doNotCopyRecords   | true/false (`boolean`)            | If true, Contao will not duplicate records of the current table when a record of its parent table is duplicated.                                |
| doNotDeleteRecords | true/false (`boolean`)            | If true, Contao will not delete records of the current table when a record of its parent table is deleted.                                      |
| onload_callback    | Callback function (`array`)       | Calls a custom function when a DataContainer is initialized and passes the DataContainer object as argument.                                    |
| onsubmit_callback  | Callback function (`array`)       | Calls a custom function after a record has been updated and passes the DataContainer object as argument.                                        |
| ondelete_callback  | Callback function (`array`)       | Calls a custom function when a record is deleted and passes the DataContainer object as argument.                                               |
| oncut_callback     | Callback function (`array`)       | Calls a custom function when a record is moved and passes the DataContainer object as argument. Added in version 2.8.2.                         |
| oncopy_callback    | Callback function (`array`)       | Calls a custom function when a record is duplicated and passes the insert ID and the DataContainer object as argument. Added in version 2.8.2.  |
| onversion_callback | Callback function (`array`)       | Calls a custom function when a new version of a record is created and passes the table, the insert ID and the DataContainer object as argument. |
| onrestore_callback | Callback function (`array`)       | Calls a custom function when a version of a record is restored and passes the insert ID, the table, the data array and the version as argument. |
| sql                | Table configuration (`array`)     | Describes table configuration, e.g. `'keys' => array ( 'id' => 'primary', 'pid' => 'index' )`                                                   |


### Listing records

The listing array defines how records are listed. The Contao core engine
supports three different [views][1]: "list view", "parent view" and "tree view".
You can configure various sorting options like filters or the default sorting
order and you can add custom labels.


#### Sorting

| Key                   | Value                            | Description                                                                                                                                                                                                                                                                                                                                                                                            |
|-----------------------|----------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| mode                  | Sorting mode (`integer`)         | **0** Records are not sorted **1** Records are sorted by a fixed field **2** Records are sorted by a switchable field **3** Records are sorted by the parent table **4** Displays the child records of a parent record (see style sheets module) **5** Records are displayed as tree (see site structure) **6** Displays the child records within a tree structure (see articles module)               |
| flag                  | Sorting flag (`integer`)         | **1** Sort by initial letter ascending **2** Sort by initial letter descending **3** Sort by initial two letters ascending **4** Sort by initial two letters descending **5** Sort by day ascending **6** Sort by day descending **7** Sort by month ascending **8** Sort by month descending **9** Sort by year ascending **10** Sort by year descending **11** Sort ascending **12** Sort descending |
| panelLayout           | Panel layout (`string`)          | **search** show the search records menu **sort** show the sort records menu **filter** show the filter records menu **limit** show the limit records menu. Separate options with comma (= space) and semicolon (= new line) like `sort,filter;search,limit`.                                                                                                                                           |
| fields                | Default sorting values (`array`) | One or more fields that are used to sort the table.                                                                                                                                                                                                                                                                                                                                                    |
| headerFields          | Header fields (`array`)          | One or more fields that will be shown in the header element (sorting mode 4 only).                                                                                                                                                                                                                                                                                                                     |
| icon                  | Tree icon (`string`)             | Path to an icon that will be shown on top of the tree (sorting mode 5 and 6 only).                                                                                                                                                                                                                                                                                                                     |
| root                  | Root nodes (`array`)             | IDs of the root records (pagemounts). This value usually takes care of itself.                                                                                                                                                                                                                                                                                                                         |
| rootPaste             | true/false (`boolean`)           | Override disabling paste buttons to root, if root is set. (default: false)                                                                                                                                                                                                                                                                                                                             |
| filter                | Query filter (`array`)           | Allows you to add custom filters as arrays, e.g. `array('status=?', 'active')`.                                                                                                                                                                                                                                                                                                                        |
| disableGrouping       | true/false (`boolean`)           | Allows you to disable the group headers in list view and parent view.                                                                                                                                                                                                                                                                                                                                  |
| paste_button_callback | Callback function (`array`)      | This function will be called instead of displaying the default paste buttons. Please specify as `array('Class', 'Method')`.                                                                                                                                                                                                                                                                            |
| child_record_callback | Callback function (`array`)      | This function will be called to render the child elements (sorting mode 4 only). Please specify as `array('Class', 'Method')`.                                                                                                                                                                                                                                                                         |
| child_record_class    | CSS class (`string`)             | Allows you to add a CSS class to the parent view elements.                                                                                                                                                                                                                                                                                                                                             |


#### Labels

| Key            | Value                            | Description                                                                                        |
|----------------|----------------------------------|----------------------------------------------------------------------------------------------------|
| fields         | Fields (`array`)                 | One or more fields that will be shown in the list (e.g. `array('title', 'user_id:tl_user.name')`). |
| showColumns    | true/false (`boolean`)           | If true Contao will generate a table header with column names (e.g. back end member list)          |
| format         | Format string (`string`)         | HTML string used to format the fields that will be shown (e.g. **%s** ).                           |
| maxCharacters  | Number of characters (`integer`) | Maximum number of characters of the label.                                                         |
| group_callback | Callback function (`array`)      | Call a custom function instead of using the default group header function.                         |
| label_callback | Callback function (`array`)      | Call a custom function instead of using the default label function.                                |


### Operations

The operations array is divided into two sections: global operations that relate
to all records at once (e.g. editing multiple records) and regular operations
that relate to a particular record only (e.g. editing or deleting a record).


#### Global operations

| Key             | Value                             | Description                                                                                                        |
|-----------------|-----------------------------------|--------------------------------------------------------------------------------------------------------------------|
| label           | `&$GLOBALS['TL_LANG']` (`string`) | Button label. Typically a reference to the global language array.                                                  |
| href            | URL fragment (`string`)           | URL fragment that is added to the URI string when the button is clicked (e.g. `act=editAll`).                      |
| class           | CSS class (`string`)              | CSS class attribute of the button.                                                                                 |
| attributes      | Additional attributes (`string`)  | Additional attributes like event handler or style definitions.                                                     |
| button_callback | Callback function (`array`)       | Call a custom function instead of using the default button function. Please specify as `array('Class', 'Method')`. |


#### Regular operations

| Key             | Value                             | Description                                                                                                        |
|-----------------|-----------------------------------|--------------------------------------------------------------------------------------------------------------------|
| label           | `&$GLOBALS['TL_LANG']` (`string`) | Button label. Typically a reference to the global language array.                                                  |
| href            | URL fragment (`string`)           | URL fragment that is added to the URI string when the button is clicked (e.g. `act=edit`).                         |
| icon            | Icon (`string`)                   | Path and filename of the icon.                                                                                     |
| attributes      | Additional attributes (`string`)  | Additional attributes like event handler or style definitions.                                                     |
| button_callback | Callback function (`array`)       | Call a custom function instead of using the default button function. Please specify as `array('Class', 'Method')`. |


### Fields

The fields array defines the columns of a table. Depending on these settings,
the Contao core engine decides which type of form field to load, whether a user
is allowed to access a certain field and whether a field can be used as sort or
filter criteria.

| Key                  | Value                                           | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
|:---------------------|:------------------------------------------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| label                | `&$GLOBALS['TL_LANG']` (`string`)               | Field label. Typically a reference to the global language array.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| default              | Default value (`mixed`)                         | Default value that is set when a new record is created.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| exclude              | true/false (`boolean`)                          | If true the field will be excluded for non-admins. It can be enabled in the user group module (allowed excluded fields).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| search               | true/false (`boolean`)                          | If true the field will be included in the search menu (see "sorting records" -> "panelLayout").                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| sorting              | true/false (`boolean`)                          | If true the field will be included in the sorting menu (see "sorting records" -> "panelLayout").                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| filter               | true/false (`boolean`)                          | If true the field will be included in the filter menu (see "sorting records" -> "panelLayout").                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| flag                 | Sorting mode (`integer`)                        | **1** Sort by initial letter ascending **2** Sort by initial letter descending **3** Sort by initial X letters ascending (see length) **4** Sort by initial X letters descending (see length) **5** Sort by day ascending **6** Sort by day descending **7** Sort by month ascending **8** Sort by month descending **9** Sort by year ascending **10** Sort by year descending **11** Sort ascending **12** Sort descending                                                                                                                                                                                                                    |
| length               | Sorting length (`integer`)                      | Allows to specify the number of characters that are used to build sorting groups (flag 3 and 4).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| inputType            | Field type (`string`)                           | **text** Text field **password** Password field **textarea** Textarea **select** Drop-down menu **checkbox** Checkbox **radio** Radio button **radioTable** Table with images and radio buttons **imageSize** Two text fields with drop-down menu **inputUnit** Text field with small unit drop-down menu **trbl** Four text fields with a small unit drop-down menu **chmod** CHMOD table **pageTree** Page tree **fileTree** File tree **tableWizard** Table wizard **timePeriod** Text field with drop-down menu **listWizard** List wizard **optionWizard** Option wizard **moduleWizard** Module wizard **checkboxWizard** Checkbox Wizard |
| options              | Options (`array`)                               | Options of a drop-down menu or radio button menu.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| options_callback     | Callback function (`array`)                     | Callback function that returns an array of options. Please specify as `array('Class', 'Method')`.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| foreignKey           | table.field (`string`)                          | Get options from a database table. Returns ID as key and the field you specify as value.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| reference            | `&$GLOBALS['TL_LANG']` (`string`)               | Array that holds the options labels. Typically a reference to the global language array.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| explanation          | `&$GLOBALS['TL_LANG']` (`string`)               | Array that holds the explanation. Typically a reference to the global language array.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| input_field_callback | Callback function (`array`)                     | Executes a custom function instead of using the default input field routine and passes the the DataContainer object and the label as arguments.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| eval                 | Field configuration (`array`)                   | Various configuration options. See next paragraph.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| wizard               | Callback function (`array`)                     | Call a custom function and add its return value to the input field. Please specify as `array('Class', 'Method')`.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| sql                  | Database field definition (`string` or `array`) | Describes data type and its database configuration. (see paragraph [SQL Column Definition](#sql-column-definition)).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| relation             | Configuration of relations (`array`)            | Describes relation to parent table (see paragraph [Relations](#relations)).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| load_callback        | Callback functions (`array`)                    | These functions will be called when the field is loaded. Please specify each callback function as `array('Class', 'Method')`. Passes the field's value and the data container as arguments. Expects the field value as return value.                                                                                                                                                                                                                                                                                                                                                                                                            |
| save_callback        | Callback functions (`array`)                    | These functions will be called when the field is saved. Please specify each callback function as `array('Class', 'Method')`. Passes the field's value and the data container as arguments. Expects the field value as return value. Throw an exception to display an error message.                                                                                                                                                                                                                                                                                                                                                             |


### Evaluation

The evaluation array configures a particular field in detail. You can e.g.
create mandatory fields, add a date picker or define the rows and columns of a
textarea. You can also modify the field appearance or enable data encryption.
Each field can be validated against a regular expression.

| Key                | Value                            | Description                                                                                                                                                              |
|:-------------------|:---------------------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| helpwizard         | true/false (`boolean`)           | If true the helpwizard icon will appear next to the field label.                                                                                                         |
| mandatory          | true/false (`boolean`)           | If true the field cannot be empty.                                                                                                                                       |
| maxlength          | Maximum length (`integer`)       | Maximum number of characters that is allowed in the current field.                                                                                                       |
| minlength          | Minimum length (`integer`)       | Minimum number of characters that have to be entered.                                                                                                                    |
| maxval             | Maximum value (`integer`)        | Maximum number value to be checked (upper bound).                                                                                                                        |
| minval             | Minimum value (`integer`)        | Minimum number value to be checked (lower bound).                                                                                                                        |
| fallback           | true/false (`boolean`)           | If true the field can only be assigned once per table.                                                                                                                   |
| rgxp               | Regular expression (`string`)    | Limits the user input to certain rules (see paragraph [Regular Expressions](#regular-expressions)).                                                                      |
| cols               | Columns (`integer`)              | Number of columns (textarea fields only).                                                                                                                                |
| rows               | Rows (`integer`)                 | Number of rows (textarea fields only).                                                                                                                                   |
| multiple           | true/false (`boolean`)           | Make the input field multiple. Applies to text fields, select menus, radio buttons and checkboxes. Required for the checkbox wizard.                                     |
| size               | Size (`integer`)                 | Size of a multiple select menu or number of input fields.                                                                                                                |
| style              | Style attributes (`string`)      | Style attributes (e.g. `border:2px`).                                                                                                                                    |
| rte                | Rich text editor file (`string`) | **tinyMCE** use file `config/tinyMCE.php`. **tinyFlash** use file `config/tinyFlash.php`. You can add your own configuration files too.                                  |
| submitOnChange     | true/false (`boolean`)           | If true the form will be submitted when the field value changes.                                                                                                         |
| nospace            | true/false (`boolean`)           | If true whitespace characters will not be allowed.                                                                                                                       |
| allowHtml          | true/false (`boolean`)           | If true the current field will accept HTML input (see "Allowed HTML tags" in the backend System => Settings).                                                            |
| preserveTags       | true/false (`boolean`)           | If true no HTML tags will be removed at all.                                                                                                                             |
| decodeEntities     | true/false (`boolean`)           | If true HTML entities will be decoded. Note that HTML entities are always decoded if allowHtml is true.                                                                  |
| doNotSaveEmpty     | true/false (`boolean`)           | If true the field will not be saved if it is empty.                                                                                                                      |
| alwaysSave         | true/false (`boolean`)           | If true the field will always be saved, even if its value has not changed. This can be useful in conjunction with a load_callback.                                       |
| spaceToUnderscore  | true/false (`boolean`)           | If true any whitespace character will be replaced by an underscore.                                                                                                      |
| unique             | true/false (`boolean`)           | If true the field value cannot be saved if it exists already.                                                                                                            |
| encrypt            | true/false (`boolean`)           | If true the field value will be stored encrypted.                                                                                                                        |
| trailingSlash      | true/false (`boolean`)           | If true a trailing slash will be added to the field value. If false, an existing trailing slash will be removed from the field value.                                    |
| files              | true/false (`boolean`)           | If true files and folders will be shown. If false, only folders will be shown. Applies to file trees only.                                                               |
| filesOnly          | true/false (`boolean`)           | Removes the radio buttons or checkboxes next to folders. Applies to file trees only.                                                                                     |
| extensions         | File extensions (`string`)       | Limits the file tree to certain file types (comma separated list). Applies to file trees only.                                                                           |
| path               | Path (`string`)                  | Custom root directory for file trees. Applies to file trees only.                                                                                                        |
| fieldType          | Input field type (`string`)      | **checkbox** allow multiple selections **radio** allow a single selection only Applies to file and page trees only.                                                      |
| includeBlankOption | true/false (`boolean`)           | If true a blank option will be added to the options array. Applies to drop-down menus only.                                                                              |
| blankOptionLabel   | Label (`string`)                 | Label for the blank option (defaults to `-`).                                                                                                                            |
| chosen             | true/false (`boolean`)           | Native selects enhanced with [Chosen](http://harvesthq.github.io/chosen/).                                                                                               |
| findInSet          | true/false (`boolean`)           | Sort by the actual option values instead of their labels.                                                                                                                |
| datepicker         | true/false (`boolean`)           | If true the current field has a date picker.                                                                                                                             |
| colorpicker        | true/false (`boolean`)           | If true the current field has a color picker.                                                                                                                            |
| feEditable         | true/false (`boolean`)           | If true the current field can be edited in the front end. Applies to table `tl_member` only.                                                                             |
| feGroup            | Group name (`string`)            | **personal** personal data **address** address details **contact** contact details **login** login details (table `tl_member` only) You can also define your own groups. |
| feViewable         | true/false (`boolean`)           | If true the current field is viewable in the member listing module.                                                                                                      |
| doNotCopy          | true/false (`boolean`)           | If true the current field will not be duplicated if the record is duplicated.                                                                                            |
| hideInput          | true/false (`boolean`)           | If true the field value will be hidden (it is still visible in the page source though!).                                                                                 |
| doNotShow          | true/false (`boolean`)           | If true the current field will not be shown in "edit all" or "show details" mode.                                                                                        |
| isBoolean          | true/false (`boolean`)           | Indicates that a particular field is boolean.                                                                                                                            |
| disabled           | true/false (`boolean`)           | Disables the field (not supported by all field types).                                                                                                                   |
| readonly           | true/false (`boolean`)           | Makes the field read only (not supported by all field types).                                                                                                            |
| csv                | Delimiter (`string`)             | The choice of this field will not be stored as serialized string but rather as given delimiter-separated list. Example: `'eval' => array('csv'=>',')`                    |
| tl_class           | CSS class(es) (`string`)         | Add the given CSS class(es) to the generated HTML. See section [Arranging Fields](palettes.md#arranging-fields) for supported values.                                    |


### Regular Expressions

Regular expressions requires the input of a field to match a pre-defined format.
A lot of useful formats are shipped with Contao, but additional formats
can be [registered using a hook][3].


| Key         | Description                                                                                                       |
|:------------|:------------------------------------------------------------------------------------------------------------------|
| digit       | allows numeric characters only (including full stop [.] and minus [-])                                            |
| natural     | allows non-negative natural numbers (including 0)                                                                 |
| alpha       | allows alphabetic characters only (including full stop [.] minus [-] and space [ ])                               |
| alnum       | allows alphanumeric characters only (including full stop [.] minus [-], underscore [_] and space [ ])             |
| extnd       | disallows `#<>()\\=`                                                                                              |
| date        | expects a valid date                                                                                              |
| time        | expects a valid time                                                                                              |
| datim       | expects a valid date and time                                                                                     |
| friendly    | expects a valid "friendly name format" e-mail address                                                             |
| email       | expects a valid e-mail address                                                                                    |
| emails      | expects a valid list of valid e-mail addresses                                                                    |
| url         | expects a valid URL                                                                                               |
| alias       | expects a valid alias                                                                                             |
| folderalias | expects a valid folder URL alias                                                                                  |
| phone       | expects a valid phone number (numeric characters, space [ ], plus [+], minus [-], parentheses [()] and slash [/]) |
| prcnt       | allows numbers between 0 and 100                                                                                  |
| locale      | expects a valid locale (e.g. "de-CH")                                                                             |
| language    | expects a valid language code                                                                                     |
| google+     | expects a Google+ ID or vanity name                                                                               |
| fieldname   | expects a valid field name (added in version 3.5.16 / 4.2.3)                                                      |


### Relations

Relations describe, how database fields are related to other tables.
Define the referenced table in the `foreignKey` key. Relations provide
model classes to load referenced data sets efficiently and developer friendly.
(see `Model::getRelated()`).

| Key   | Value                           | Description                                                                                                                                                                                                                                     |
|-------|---------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| type  | Type of relation (`string`)     | **hasOne** Value references a child data set **hasMany** Value references some child data sets (serialized) **belongsTo** Value references a parent data set (e.g. `pid`) **belongsToMany** Value references some parent data sets (serialized) |
| load  | Load behaviour (`string`)       | **lazy** Loading referenced records only when necessary (default, saves RAM) **eager** Loading referenced records automatically (saves database calls)                                                                                          |
| table | Relation table (`string`)       | A database table for this relation. Optional, by default Contao tries to extract it from the `foreignKey` attribute.                                                                                                                            |
| field | Relation table field (`string`) | Override the default relation field (`id`). Useful for relation with `tl_files.uuid` for example.                                                                                                                                               |


### SQL Column Definition

Since Contao 3.0, the database definition is added as a string to each DCA
field, e.g. `varchar(255) NOT NULL default ''`. Starting from Contao 4.3,
one can use [Doctrine Schema Representation][2] to take full advantage of
the Doctrine Database Abstraction Layer.

**Examples:**

| Doctrine Schema Representation                                          | SQL Equivalent                    |
|:------------------------------------------------------------------------|:----------------------------------|
| `['type' => 'string', 'length' => 32, 'default' => '']`                 | `varchar(32) NOT NULL default ''` |
| `['type' => 'string', 'length' => 1, 'fixed' => true, 'default' => '']` | `char(1) NOT NULL default ''`     |
| `['type' => 'integer', 'notnull' => false, 'unsigned' => true]`         | `INT unsigned NULL`               |



[1]: https://docs.contao.org/books/manual/current/en/02-administration-area/listing-records.html
[2]: http://docs.doctrine-project.org/projects/doctrine-dbal/en/latest/reference/schema-representation.html#column
[3]: ../extensions/hooks/addCustomRegexp.md
