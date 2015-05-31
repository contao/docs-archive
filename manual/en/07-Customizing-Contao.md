# Customizing Contao

Customizability is one of the most important features of any application and
particularly Content Management Systems. Contao provides many options to adjust
the configuration, customize fields and labels, add own code snippets or even
create new extensions. You can control almost any behaviour of the Contao core
without even touching its files, so you do not have to reapply your changes
after every update.


## Bypass the internal cache 

Before developing extensions for Contao, you should bypass the internal cache.
If you want to bypass the internal cache, navigate to "System" -> "Settings" and 
enable the checkbox "Bypass the internal cache" under "Global configuration".

![](images/bypass-internal-cache.jpg?raw=true)

As soon as the site goes into production, you should uncheck "Bypass the 
internal cache" in order to minimize the response time.  


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

``` {.php}
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

``` {.php}
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

``` {.php}
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

``` {.php}
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
[Contao install tool][3] in order to update your database tables.


### Adding a translation

Create the file `languages/en/tl_member.php` in your module folder and add the
English labels for the new field:

``` {.php}
$GLOBALS['TL_LANG']['tl_member']['customer_number'] = array
(
    'Customer number',
    'Please enter the 8-digit customer number.'
);
```

Now you can enter a customer number in the "members" module which can contain up
to 8 digits. If the field is left blank or contains any non-digit characters,
Contao will not save the value and show an error message instead.


## Customizing TinyMCE

This page explains how to customize the Rich Text Editor and save the changes so
they will not be overridden on the next Contao update. Note that Contao does not
include all TinyMCE plugins by default, so if you want to use a certain plugin
that is not part of the Contao distribution, download it from the [TinyMCE
project website][4] and move it into the `assets/tinymce/plugins` folder.

![](images/rich-text-editor.jpg?raw=true)

The image above shows the default Rich Text Editor configuration file
`system/config/tinyMCE.php`. To create a custom configuration file, simply copy
it and rename it e.g. to `tinyCustom.php`. Then apply your changes and save the
new file. The last step is to adjust the [data container configuration][5] in
the `system/config/dcaconfig.php` file and tell Contao to which fields the
custom file shall be applied.

``` {.php}
// Use the custom RTE configuration for text elements
$GLOBALS['TL_DCA']['tl_content']['fields']['text']['eval']['rte'] =
'tinyCustom';
```


## Overriding class methods

Let us assume that you want to modify the behaviour of the navigation module to
always display even if there are no sub-pages and the module would not be shown
at all. In this case a note shall be printed to inform the user that there are
no sub-pages. Of course we will try to preserve as much of the original
navigation class as possible, so future updates do not require maintenance.
Module and content element classes can be assigned dynamically in the Contao
system configuration, which allows you to easily replace them with your own
versions.


### Creating a custom class

The default navigation class behaves pretty much like we want it to, except that
the `generate()` method hides the module if there are no sub-pages. Therefore
all we need to change is this particular method, so the best practice is to
extend the original class and simply override it. To do so, create a new
`xcustom/ModuleMyNavigation.php` file and define the custom class
`ModuleMyNavigation`:

``` {.php}
// xcustom/ModuleMyNavigation.php
class ModuleMyNavigation extends ModuleNavigation
{
    public function generate()
    {
        // Execute the original method
        $buffer = parent::generate();

        if (empty($buffer))
        {
            $buffer = 'There are no subpages';
        }

        return $buffer;
    }
}
```


### Registering a custom class

Module and content element classes can be assigned dynamically in the Contao
system configuration, which allows you to easily replace them with your own
versions. The names of the module classes are stored in the global `FE_MOD`
array.

``` {.php}
// xcustom/config/config.php
$GLOBALS['FE_MOD']['navigationMenu']['navigation'] = 'ModuleMyNavigation';
```

Thanks to the dynamic configuration, Contao automatically loads the new class
upon the next request and the navigation module prints the "There are no
subpages" notice instead of not displaying at all. The modification is
update-safe and does not require maintenance.


## Contao hooks

Hooks work similar to the [callback functions][6] of the Data Container Array.
You can register one or more functions for a certain event and when the event is
triggered, the callback functions are executed. Hooks allow you to add custom
functionality to the core.


### activateAccount

The "activateAccount" hook is triggered when a new front end account is
activated. It passes the user object as argument and does not expect a return
value. It is available from version 2.4.3.

``` {.php}
// config.php
$GLOBALS['TL_HOOKS']['activateAccount'][] = array('MyClass',
'myActivateAccount');

// MyClass.php
public function myActivateAccount(Database_Result $objUser)
{
    // Do something
}
```


### activateRecipient

The "activateRecipient" hook is triggered when a new newsletter recipient is
added. It passes the e-mail address, the recipient IDs and the channel IDs as
argument and does not expect a return value. It is available from version
2.8.RC1.

``` {.php}
// config.php
$GLOBALS['TL_HOOKS']['activateRecipient'][] = array('MyClass',
'myActivateRecipient');

// MyClass.php
public function myActivateRecipient($strEmail, $arrRecipients, $arrChannels)
{
    // Do something
}
```


### addComment

The "addComment" hook is triggered when a comment is added. It passes the ID of
the record and the data array as arguments and does not expect a return value.
It is available from version 2.8.2.

``` {.php}
// config.php
$GLOBALS['TL_HOOKS']['addComment'][] = array('MyClass', 'myAddComment');

// MyClass.php
public function myAddComment($intId, $arrSet)
{
    // Do something
}
```


### addCustomRegexp

The "addCustomRegexp" hook is triggered when an unknown regular expression is
found. It passes the name of the regexp, the current value and the widget object
as arguments and expects a boolean return value. It is available from version
2.6.2.

``` {.php}
// config.php
$GLOBALS['TL_HOOKS']['addCustomRegexp'][] = array('MyClass',
'myAddCustomRegexp');

// MyClass.php
public function myAddCustomRegexp($strRegexp, $varValue, Widget $objWidget)
{
    if ($strRegexp == 'postal')
    {
        if (!preg_match('/^0-9{4,6}$/', $varValue))
        {
            $objWidget->addError('Field ' . $objWidget->label . ' should be a postal code.');
        }

        return true;
    }

    return false;
}
```


### addLogEntry

The "addLogEntry" hook is triggered when a new log entry is added. It passes the
message, the function and the action as arguments and does not expect a return
value. It is available from version 2.8.RC1.

``` {.php}
// config.php
$GLOBALS['TL_HOOKS']['addLogEntry'][] = array('MyClass', 'myAddLogEntry');

// MyClass.php
public function myAddLogEntry($strText, $strFunction, $strAction)
{
    // Do something
}
```


### checkCredentials

The "checkCredentials" hook is triggered when a login attempt fails due to a
wrong password. It passes the username and password as well as the user object
as arguments and expects a boolean return value. It is available from version
2.6.0.

``` {.php}
// config.php
$GLOBALS['TL_HOOKS']['checkCredentials'][] = array('MyClass',
'myCheckCredentials');

// MyClass.php
public function myCheckCredentials($strUsername, $strPassword, User $objUser)
{
    // Check against a global database
    if ($this->checkGlobalDbFor($strUsername, $strPassword))
    {
        return true;
    }

    return false;
}
```


### closeAccount

The "closeAccount" hook is triggered when a user closes his account. It passes
the user ID, the operation mode and the module as arguments and does not expect
a return value. It is available from version 2.8.0.

``` {.php}
// config.php
$GLOBALS['TL_HOOKS']['closeAccount'][] = array('MyClass', 'myCloseAccount');

// MyClass.php
public function myCloseAccount($intId, $strMode, $objModule)
{
    if ($strMode == 'close_delete')
    {
        // Do something
    }
}
```


### colorizeLogEntries
The "colorizeLogEntries" hook is triggered in the label callback for tl_log entries. 
It passes an array holding the current row data and the current label and expects a
HTML string as return value. You can use it to generate custom labels for custom 
log categories, but you may also modify existing labels. It is available from 
Version 3.3.RC1.

``` {.php}
// config.php
$GLOBALS['TL_HOOKS']['colorizeLogEntries'][] = array('MyClass', 'colorizeLogEntries');

// MyClass.php
public function colorizeLogEntries($row, $label)
{
    // Do something
}
```


### compileDefinition

The "compileDefinition" hook is triggered when a format definition of a style
sheet is written. It passes the configuration array as argument and expects a
string as return value. It is available from version 2.9.4.

``` {.php}
// config.php
$GLOBALS['TL_HOOKS']['compileDefinition'][] = array('MyClass',
'myCompileDefinition');

// MyClass.php
public function myCompileDefinition($arrRow)
{
    if (isset($arrRow['border-radius']))
    {
        return "\nborder-radius:" . $arrRow['border-radius'] . ";";
    }

    return '';
}
```


### compileFormFields

The "compileFormFields" hook is triggered before a form field is loaded. 
It passes an array of FormFieldModel objects, the form ID and the form object as 
arguments and expects the array of FormFieldModel objects as return value. 
With this Hook form fields can be adjusted dynamically before display.
It is available from version 3.2.

``` {.php}
// config.php
$GLOBALS['TL_HOOKS']['compileFormFields'][] = array('MyClass', 'myCompileFormFields');

// MyClass.php
public function myCompileFormFields($arrFields, $formId, $this)
{
    if ($formId == 'my_form_id') 
    {
        foreach ($arrFields AS $objFields) 
        {
		if($objFields->name == 'my_form_field_1') 
		{
			// Do something
        	}
	}
    }
    
    return $arrFields;
}
```


### createDefinition

The "createDefinition" hook is triggered when a format definition of a style
sheet is imported. It passes the key and value, the original format definition
and the data array as arguments and expects an array or "false" as return value.
It is available from version 2.9.4.

``` {.php}
// config.php
$GLOBALS['TL_HOOKS']['createDefinition'][] = array('MyClass',
'myCreateDefinition');

// MyClass.php
public function myCreateDefinition($strKey, $strValue, $strDefinition, $arrSet)
{
    if ($strKey == 'border-radius')
    {
        return array('border-radius'=>$strValue);
    }

    return false;
}
```


### createNewUser

The "createNewUser" hook is triggered when a new front end user registers on the
website. It passes the ID of the new user and the data array as arguments and
does not expect a return value. It is available from version 2.2.0.

``` {.php}
// config.php
$GLOBALS['TL_HOOKS']['createNewUser'][] = array('MyClass', 'myCreateNewUser');

// MyClass.php
public function myCreateNewUser($intId, $arrData)
{
    // Modify the record
}
```


### executePreActions

The "executePreActions" hook is triggered on Ajax requests that do not require a
DCA object. It passes the name of the action as argument and does not expect a
return value. It is available from version 2.6.1.

``` {.php}
// config.php
$GLOBALS['TL_HOOKS']['executePreActions'][] = array('MyClass', 'myExecutePreActions');

// MyClass.php
public function myExecutePreActions($strAction)
{
    if ($strAction == 'update')
    {
        // Do something
    }
}
```


### executePostActions

The "executePostActions" hook is triggered on Ajax requests that require a DCA
object. It passes the name of the action and the data container object as
arguments and does not expect a return value. It is available from version
2.6.1.

``` {.php}
// config.php
$GLOBALS['TL_HOOKS']['executePostActions'][] = array('MyClass', 'myExecutePostActions');

// MyClass.php
public function myExecutePostActions($strAction, DataContainer $dc)
{
    if ($strAction == 'update')
    {
        // Do something
    }
}
```


### generateBreadcrumb

The "generateBreadcrumb" hook allows to modify the breadcrumb navigation.
It passes the navigation items and the frontend module as arguments and expects
the items as return value. It is available from version 2.10.0.

``` {.php}
// config.php
$GLOBALS['TL_HOOKS']['generateBreadcrumb'][] = array('MyClass', 'myGenerateBreadcrumb');

// MyClass.php
public function myGenerateBreadcrumb($arrItems, \Module $objModule)
{
	return $arrItems;
}
```


### generateFrontendUrl

The "generateFrontendUrl" hook is triggered when a front end URL is recreated.
It passes the page object, the parameter string and the default URL as arguments
and expects a string as return value. It is available from version 2.5.8.

``` {.php}
// config.php
$GLOBALS['TL_HOOKS']['generateFrontendUrl'][] = array('MyClass', 'myGenerateFrontendUrl');

// MyClass.php
public function myGenerateFrontendUrl($arrRow, $strParams, $strUrl)
{
    return str_replace('.html', '.xml', $strUrl);
}
```


### generatePage

The "generatePage" hook is triggered before the main layout ("fe_page") is
compiled. It passes the page object, the layout object and a self-reference as
arguments and does not expect a return value. It is available from version
2.8.RC1.

``` {.php}
// config.php
$GLOBALS['TL_HOOKS']['generatePage'][] = array('MyClass', 'myGeneratePage');

// MyClass.php
public function myGeneratePage(\PageModel $objPage, \LayoutModel $objLayout, \PageRegular $objPageRegular)
{
    // Do something
}
```


### getAllEvents

The "getAllEvents" hook allows you to modify the result sets of calendar and
event modules. It passes the current result set, the IDs of the parent items and
the start and end time as arguments and expects a result set (array) as return
value. It is available from version 2.6.4.

``` {.php}
// config.php
$GLOBALS['TL_HOOKS']['getAllEvents'][] = array('MyClass', 'myGetAllEvents');

// MyClass.php
public function myGetAllEvents($arrEvents, $arrCalendars, $intStart, $intEnd, Module $objModule)
{
    ksort($arrEvents);
    return $arrEvents;
}
```


### getContentElement

The "getContentElement" hook is triggered when a content element is rendered. It
passes the database object and the buffer string as arguments and expects a
buffer string as return value. It is available from version 2.9.0.

``` {.php}
// config.php
$GLOBALS['TL_HOOKS']['getContentElement'][] = array('MyClass', 'myGetContentElement');

// MyClass.php
public function myGetContentElement(Database_Result $objElement, $strBuffer)
{
    return $strBuffer;
}
```


### getImage

The "getImage" hook is triggered when a thumbnail is generated and allows you to
add a custom routine. It passes the path, the width and height, the mode, the
cache name and the file object as arguments and expects a path as return value.
It is available from version 2.8.RC1.

``` {.php}
// config.php
$GLOBALS['TL_HOOKS']['getImage'][] = array('MyClass', 'myGetImage');

// MyClass.php
public function myGetImage($image, $width, $height, $mode, $strCacheName, $objFile)
{
    return MyImage::generateThumbnail($image, $widht, $height, $mode);
}
```


### getPageIdFromUrl

The "getPageIdFromUrl" hook is triggered when the URL fragments are evaluated.
It passes the array of URL fragments as argument and expects an array of URL
fragments as return value. It is available from version 2.5.4.

``` {.php}
// config.php
$GLOBALS['TL_HOOKS']['getPageIdFromUrl'][] = array('MyClass', 'myGetPageIdFromUrl');

// MyClass.php
public function myGetPageIdFromUrl($arrFragments)
{
    return array_unique($arrFragments);
}
```


### getPageLayout

The "getPageLayout" hook is executed before initializing the frontend template.
It passes the page model, the layout object and a reference to the page object
and does not expect a return value. It is available from version 3.1.0.

``` {.php}
// config.php
$GLOBALS['TL_HOOKS']['getPageLayout'][] = array('MyClass', 'mygetPageLayout');

// MyClass.php
public function mygetPageLayout(\PageModel $objPage, \LayoutModel $objLayout, \PageRegular $objPageRegular)
{
    // Do something
}
```


### getSearchablePages

The "getSearchablePages" hook is triggered when the the search index is rebuilt.
It passes the array of pages and the ID of the root page as arguments and
expects an array of absolute URLs (!) as return value. It is available from
version 2.2.0.

``` {.php}
// config.php
$GLOBALS['TL_HOOKS']['getSearchablePages'][] = array('MyClass', 'myGetSearchablePages');

// MyClass.php
public function myGetSearchablePages($arrPages, $intRoot)
{
    return array_merge($arrPages, array('Additional pages'));
}
```


### initializeSystem

The "initializeSystem" hook is triggered when the system is initialized. It is
available from version 3.1.RC1.

``` {.php}
// config.php
$GLOBALS['TL_HOOKS']['initializeSystem'][] = array('MyClass', 'myInitializeSystem');

// MyClass.php
public function myInitializeSystem()
{
    // Do something
}
```


### importUser

The "importUser" hook is triggered when a username cannot be found in the
database. It passes the username, the password and the table name as arguments
and expects a boolean return value. It is available from version 2.7.RC1.

``` {.php}
// config.php
$GLOBALS['TL_HOOKS']['importUser'][] = array('MyClass', 'myImportUser');

// MyClass.php
public function myImportUser($strUsername, $strPassword, $strTable)
{
    if ($strTable == 'tl_member')
    {
        // Import user from an LDAP server
        if ($this->importUserFromLdap($strUsername, $strPassword))
        {
            return true;
        }
    }

    return false;
}
```


### isVisibleElement

The "isVisibleElement" hook is triggered when checking if an element should be
visible in the front end or not. An "element" in this case means either an
article, a front end module or a content element. In contrast to the other three
hooks "getArticle", "getFrontendModule" and "getContentElement" one can prevent
generating the complete markup. The hook passes the model of the instance and the
current visibility state as arguments and expects the new visibility state as return
value. Available from version 3.2.RC1.

``` {.php}
// config.php
$GLOBALS['TL_HOOKS']['isVisibleElement'][] = array('MyClass', 'myIsVisibleElement');

// MyClass.php
public function myIsVisibleElement($objElement, $blnIsVisible)
{
    if ($objElement instanceof ContentElement)
    {
        // Check if this content element can be shown
        if ($this->myElementCanBeShownInFrontend($objElement))
        {
            return true;
        }
    }

    // Otherwise we don't want to change the visibility state
    return $blnIsVisible;
}
```


### listComments

The "listComments" hook is triggered when comments are listed in the back end.
It passes the current record as argument and expects a string as return value.
It is available from version 2.8.RC2.

``` {.php}
// config.php
$GLOBALS['TL_HOOKS']['listComments'][] = array('MyClass', 'myListComments');

// MyClass.php
public function myListComments($arrRow)
{
    return '<a href="contao/main.php?do= … ">' . $arrRow['title'] . '</a>';
}
```


### loadFormField

The "loadFormField" hook is triggered when a form field is loaded. It passes the
widget object, the form ID and the form data as arguments and expects a widget
object as return value. It is available from version 2.5.0.

``` {.php}
// config.php
$GLOBALS['TL_HOOKS']['loadFormField'][] = array('MyClass', 'myLoadFormField');

// MyClass.php
public function myLoadFormField(Widget $objWidget, $strForm, $arrForm)
{
    $objWidget->class = 'myclass';
    return $objWidget;
}
```


### loadDataContainer

The "loadDataContainer" hook is triggered when a DCA file is loaded. It passes
the file name as argument and does not expect a return value. It is available
from version 2.8.2.

``` {.php}
// config.php
$GLOBALS['TL_HOOKS']['loadDataContainer'][] = array('MyClass', 'myLoadDataContainer');

// MyClass.php
public function myLoadDataContainer($strName)
{
    // Do something
}
```


### loadLanguageFile

The "loadLanguageFile" hook is triggered when a language file is loaded. It
passes the file name and the language as arguments and does not expect a return
value. It is available from version 2.8.RC1.

``` {.php}
// config.php
$GLOBALS['TL_HOOKS']['loadLanguageFile'][] = array('MyClass', 'myLoadLanguageFile');

// MyClass.php
public function myLoadLanguageFile($strName, $strLanguage)
{
    // Do something
}
```


### outputBackendTemplate

The "outputBackendTemplate" hook is triggered when a back end template is
printed to the screen. It passes the template content and the template name as
arguments and expects the template content as return value. It is available from
version 2.6.0.

``` {.php}
// config.php
$GLOBALS['TL_HOOKS']['outputBackendTemplate'][] = array('MyClass', 'myOutputBackendTemplate');

// MyClass.php
public function myOutputBackendTemplate($strContent, $strTemplate)
{
    if ($strTemplate == 'be_main')
    {
        // Modify output
    }

    return $strContent;
}
```


### outputFrontendTemplate

The "outputFrontendTemplate" hook is triggered when a front end template is
printed to the screen. It passes the template content and the template name as
arguments and expects the template content as return value. It is available from
version 2.6.0.

``` {.php}
// config.php
$GLOBALS['TL_HOOKS']['outputFrontendTemplate'][] = array('MyClass', 'myOutputFrontendTemplate');

// MyClass.php
public function myOutputFrontendTemplate($strContent, $strTemplate)
{
    if ($strTemplate == 'fe_page')
    {
        // Modify output
    }

    return $strContent;
}
```


### parseBackendTemplate

The "parseBackendTemplate" hook is triggered when a back end template is parsed.
It passes the template content and the template name as arguments and expects
the template content as return value. It is available from version 2.6.0.

``` {.php}
// config.php
$GLOBALS['TL_HOOKS']['parseBackendTemplate'][] = array('MyClass', 'myParseBackendTemplate');

// MyClass.php
public function myParseBackendTemplate($strContent, $strTemplate)
{
    if ($strTemplate == 'be_main')
    {
        // Modify output
    }

    return $strContent;
}
```


### parseFrontendTemplate

The "parseFrontendTemplate" hook is triggered when a front end template is
parsed. It passes the template content and the template name as arguments and
expects the template content as return value. It is available from version
2.6.0.

``` {.php}
// config.php
$GLOBALS['TL_HOOKS']['parseFrontendTemplate'][] = array('MyClass', 'myParseFrontendTemplate');

// MyClass.php
public function myParseFrontendTemplate($strContent, $strTemplate)
{
    if ($strTemplate == 'ce_text')
    {
        // Modify output
    }

    return $strContent;
}
```


### parseTemplate

The `parseTemplate` hook is called before the parsing process of a template. 
It receives a `Template` instance (can be `FrontendTemplate` or 
`BackendTemplate`) as the only parameter and does not expect any 
return value. Added in version 2.10.0.

``` {.php}
// config.php
$GLOBALS['TL_HOOKS']['parseTemplate'][] = array('MyClass', 'myParseTemplate');

// MyClass.php
public function myParseTemplate($objTemplate)
{
    if ($objTemplate->getName() == 'mod_html')
    {
        // Modify object
    }
}
```


### postDownload

The "postDownload" hook is triggered after a file has been downloaded with the
download(s) element. It passes the file name as argument and does not expect a
return value. It is available from version 2.4.6.

``` {.php}
// config.php
$GLOBALS['TL_HOOKS']['postDownload'][] = array('MyClass', 'myPostDownload');

// MyClass.php
public function myPostDownload($strFile)
{
    // Do something
}
```


### postLogin

The "postLogin" hook is triggered after a front end member or back end user
has logged in. It passes the user object as argument and does not expect
a return value.

``` {.php}
// config.php
$GLOBALS['TL_HOOKS']['postLogin'][] = array('MyClass', 'myPostLogin');

// MyClass.php
public function myPostLogin(User $objUser)
{
    // Do something
}
```


### postLogout

The "postLogout" hook is triggered after a front end member or back end user
has logged out. It passes the user object as argument and does not expect
a return value.

``` {.php}
// config.php
$GLOBALS['TL_HOOKS']['postLogout'][] = array('MyClass', 'myPostLogout');

// MyClass.php
public function myPostLogout(User $objUser)
{
    // Do something
}
```


### postUpload

The "postUpload" hook is triggered after a user has uploaded one or more file in
the back end. It passes an array of filenames as argument and does not expect a
return value. It is available from version 2.6.4.

``` {.php}
// config.php
$GLOBALS['TL_HOOKS']['postUpload'][] = array('MyClass', 'myPostUpload');

// MyClass.php
public function myPostUpload($arrFiles)
{
    // Do something
}
```

### prepareFormData

The "prepareFormData" hook is triggered after a form has been submitted. 
It passes the form data array, the form labels array and the form object as
arguments and does not expect a return value. This way the data can be 
changed or extended, prior to execution of actions like email distribution 
or data storage. It is available from version 3.0.0.

``` {.php}
// config.php
$GLOBALS['TL_HOOKS']['prepareFormData'][] = array('MyClass', 'myPrepareFormData');

// MyClass.php
public function myPrepareFormData(&$arrSubmitted, $arrLabels, $objForm)
{
    // Do something
}
```


### printArticleAsPdf

The "printArticleAsPdf" hook is triggered when an article is exported as PDF. It
passes the article text and the article object as arguments and does not expect
a return value. It is available from version 2.8.RC1.

``` {.php}
// config.php
$GLOBALS['TL_HOOKS']['printArticleAsPdf'][] = array('MyClass', 'myPrintArticleAsPdf');

// MyClass.php
public function myPrintArticleAsPdf($strArticle, Database_Result $objArticle)
{
    // Do something
    exit;
}
```


### processFormData

The "processFormData" hook is triggered after a form has been submitted. It
passes the form data array, the [Data Container Array][1] and the files array as
arguments and does not expect a return value. It is available from version
2.4.4.

``` {.php}
// config.php
$GLOBALS['TL_HOOKS']['processFormData'][] = array('MyClass', 'myProcessFormData');

// MyClass.php
public function myProcessFormData($arrPost, $arrForm, $arrFiles)
{
    // Do something
}
```


### removeOldFeeds

The "removeOldFeeds" hook is triggered when old XML files are being removed from
the Contao directory. It does not pass an argument and expects an array of file
names to preserve as return value. It is available from version 2.5.8.

``` {.php}
// config.php
$GLOBALS['TL_HOOKS']['removeOldFeeds'][] = array('MyClass', 'myRemoveOldFeeds');

// MyClass.php
public function myRemoveOldFeeds()
{
    return array('custom.xml');
}
```


### removeRecipient

The "removeRecipient" hook is triggered when a newsletter recipient is removed.
It passes the e-mail address and the channel IDs as argument and does not expect
a return value. It is available from version 2.8.RC1.

``` {.php}
// config.php
$GLOBALS['TL_HOOKS']['removeRecipient'][] = array('MyClass', 'myRemoveRecipient');

// MyClass.php
public function myRemoveRecipient($strEmail, $arrChannels)
{
    // Do something
}
```


### replaceInsertTags

The "replaceInsertTags" hook is triggered when an unknown insert tag is found.
It passes the insert tag as argument and expects the replacement value or
"false" as return value. It is available from version 2.6.0.

``` {.php}
// config.php
$GLOBALS['TL_HOOKS']['replaceInsertTags'][] = array('MyClass', 'myReplaceInsertTags');

// MyClass.php
public function myReplaceInsertTags($strTag)
{
    if ($strTag == 'mytag')
    {
        return 'mytag replacement';
    }

    return false;
}
```


### reviseTable

The "reviseTable" hook is triggered when Contao removes orphan records from a
table. It passes the name of the current table, the IDs of all new records, the
name of the parent table and the names of all child tables as arguments and does
expect a boolean return value (returning "true" will cause the current page to
be reloaded). It is available from version 2.6.4.

``` {.php}
// config.php
$GLOBALS['TL_HOOKS']['reviseTable'][] = array('MyClass', 'myReviseTable');

// MyClass.php
public function myReviseTable($table, $new_records, $parent_table, $child_tables)
{
    // Do something
}
```


### setNewPassword

The "setNewPassword" hook is triggered after a new password has been set. It
passes the user object and the encrypted password as arguments and does not
expect a return value. It is available from version 2.2.3.

``` {.php}
// config.php
$GLOBALS['TL_HOOKS']['setNewPassword'][] = array('MyClass', 'mySetNewPassword');

// MyClass.php
public function mySetNewPassword($objUser, $strPassword)
{
    // Do something
}
```


### validateFormField

The "validateFormField" hook is triggered when a form field is submitted. It
passes the widget object and the form ID as arguments and expects a widget
object as return value. It is available from version 2.5.0.

``` {.php}
// config.php
$GLOBALS['TL_HOOKS']['validateFormField'][] = array('MyClass', 'myValidateFormField');

// MyClass.php
public function myValidateFormField(Widget $objWidget, $intId)
{
    if ($objWidget instanceof FormPassword)
    {
        // Do something
    }

    return $objWidget;
}
```


[1]: 06-Data-Container-Arrays.md
[2]: http://en.wikipedia.org/wiki/List_of_ISO_639-1_codes
[3]: 01-Installation.md#the-contao-install-tool
[4]: http://tinymce.moxiecode.com
[5]: 07-Customizing-Contao.md#customizing-the-data-container-configuration
[6]: 06-Data-Container-Arrays.md#callbacks
