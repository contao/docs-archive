## Custom configurations

The Contao configuration is stored in one big array that is divided into three
sections: the system configuration, the data container configuration and the
language configuration. The configuration array is built at run-time and
contains only those parts that are required to generate a certain page. Contao
does not waste time and memory parsing a lot of redundant configuration files.


### Customizing the system configuration

The system configuration is stored in the `config.php` files of the various
Contao modules. If you want to customize it, apply your changes to the
`system/config/localconfig.php` file, so they will not be overridden on the next
update. Most parameters can be set in the back end in the settings module and
will be written to the local configuration file automatically, so you hardly
ever need to edit it manually.

```php
// Disable the extension creator
unset($GLOBALS['BE_MOD']['devtools']['extension']);

### INSTALL SCRIPT START ###
$GLOBALS['TL_CONFIG']['debugMode'] = false;
$GLOBALS['TL_CONFIG']['displayErrors'] = false;
```

Make sure to store your changes above the `INSTALL SCRIPT START` line, otherwise
they will be removed by the settings module. And **never use the `config.php`
file to store configuration parameters**, because this file might be overridden
on updates!


### Customizing the data container configuration

Contao uses [Data Container Arrays][1] to store table meta information. The data
container configuration is stored in the `dca` folders of the various Contao
modules. Apply your changes to the `system/config/dcaconfig.php` file so they
will not be overridden on the next update.

```php
// Make company a mandatory field in the members table
$GLOBALS['TL_DCA']['tl_member']['fields']['company']['eval']['mandatory'] =
true;

// Make sure that company names consist of alphanumeric characters only
$GLOBALS['TL_DCA']['tl_member']['fields']['company']['eval']['rgxp'] = 'alnum';

// Allow only admins to use include content elements
if (!BackendUser::getInstance()->isAdmin)
{
    unset($GLOBALS['TL_CTE']['includes']);
}
```

As you see, the `dcaconfig.php` file is a good place to store minor
modifications to the Contao configuration. If you need to make a lot of changes,
you should consider encapsulating them in a custom extension so you do not lose
track.


### Customizing labels and translations

Labels and translations are stored in the `languages` folders of the various
Contao modules. Each language is identified by its [ISO-639-1 language code][2].
Apply your changes to the `system/config/langconfig.php` file so they will not
be overridden on the next update.

```php
// Change a label for all languages
$GLOBALS['TL_LANG']['MSC']['goBack'] = '«';

// Change a label for a particular language only
if ($GLOBALS['TL_LANGUAGE'] == 'de')
{
    $GLOBALS['TL_LANG']['tl_layout']['column'] = 'Bereich';
}
elseif ($GLOBALS['TL_LANGUAGE'] == 'fr')
{
    $GLOBALS['TL_LANG']['tl_layout']['column'] = 'Section';
}
```

Of course changes to the language array can also be encapsulated in a custom
module, which is recommended if there are a lot of them.


[1]: https://docs.contao.org/books/manual/latest/06-data-container-arrays/README.md
[2]: http://en.wikipedia.org/wiki/List_of_ISO_639-1_codes
