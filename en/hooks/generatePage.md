generatePage
------------

The ```generatePage``` hook is triggered before the main layout (fe_page) is compiled. It passes the page object, the layout object and a self-reference as arguments and does not expect a return value. It is available from version 2.8.RC1.


### Example ###

```php
// config.php
$GLOBALS['TL_HOOKS']['generatePage'][] = array('MyClass', 'myGeneratePage');
 
// MyClass.php
public function myGeneratePage(Database_Result $objPage, Database_Result $objLayout, PageRegular $objPageRegular)
{
    // Do something
}
``` 
