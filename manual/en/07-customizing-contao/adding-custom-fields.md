## Adding custom fields

Let us assume that you want to add a customer number to the members table.
Adding a custom field to a Contao table requires to change more than just one
file, therefore it is recommended to create a custom module in the
`system/modules` directory. Remember that modules are loaded in alphabetical
order, so do not name your extension `custom` if you want to override settings
of the `news` extension.


### Extending the DCA

Create the file `dca/tl_member.php` in your module folder and add the meta data
for the new field so Contao knows how to handle it.

Since Contao 3 you can also specify directly the corresponding fields and their 
configuration for the database in the DCA under `sql`. The SQL details are not 
sent to the database but they are used to calculate the difference between the 
Contao specifications and the actual database tables.

```php
// Modify the palette
$GLOBALS['TL_DCA']['tl_member']['palettes']['default'] = str_replace
(
    'company',
    'customer_number,company',
    $GLOBALS['TL_DCA']['tl_member']['palettes']['default']
);

// Add the field meta data
$GLOBALS['TL_DCA']['tl_member']['fields']['customer_number'] = array
(
    'label'     => &amp;$GLOBALS['TL_LANG']['tl_member']['customer_number'],
    'exclude'   => true,
    'inputType' => 'text',
    'eval'      => array('mandatory'=>true, 'rgxp'=>'digit', 'maxlength'=>8),
    'sql'       => "varchar(8) NOT NULL default ''"
);
```

If you do not understand the code above, you might want to read the chapter on
[Data Container Arrays][1].

After adding or modifying a field in the DCA you should visit the 
[Contao install tool][2] in order to update your database tables.


### Adding a translation

Create the file `languages/en/tl_member.php` in your module folder and add the
English labels for the new field:

```php
$GLOBALS['TL_LANG']['tl_member']['customer_number'] = array
(
    'Customer number',
    'Please enter the 8-digit customer number.'
);
```

Now you can enter a customer number in the "members" module which can contain up
to 8 digits. If the field is left blank or contains any non-digit characters,
Contao will not save the value and show an error message instead.


[1]: 06-data-container-arrays/README.md
[2]: 01-installation/installing-contao.md#the-contao-install-tool