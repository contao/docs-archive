loadLanguageFile
----------------

The ```loadLanguageFile``` hook is triggered when a language file is loaded. It passes the file name and the language as arguments and does not expect a return value. It is available from version 2.8.RC1.


### Example ###

```php
// config.php
$GLOBALS['TL_HOOKS']['loadLanguageFile'][] = array('MyClass', 'myLoadLanguageFile');
 
// MyClass.php
public function myLoadLanguageFile($strName, $strLanguage)
{
    // Do something
}
``` 
