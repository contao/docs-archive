getContentElement
-----------------

The ```getContentElement``` hook is triggered when a content element is rendered. It passes the database object and the buffer string as arguments and expects a buffer string as return value. It is available from version 2.9.0.


### Example ###

```php
// config.php
$GLOBALS['TL_HOOKS']['getContentElement'][] = array('MyClass', 'myGetContentElement');
 
// MyClass.php
public function myGetContentElement(Database_Result $objElement, $strBuffer)
{
    return $strBuffer;
}
``` 
