generateFrontendUrl
-------------------

The generateFrontendUrl hook is triggered when a front end URL is recreated. It passes the page object, the parameter string and the default URL as arguments and expects a string as return value. It is available from version 2.5.8.

```php
// config.php
$GLOBALS['TL_HOOKS']['generateFrontendUrl'][] = array('MyClass', 'myGenerateFrontendUrl');
 
// MyClass.php
public function myGenerateFrontendUrl($arrRow, $strParams, $strUrl)
{
    return str_replace('.html', '.xml', $strUrl);
}
``` 
