validateFormField
-----------------

The validateFormField hook is triggered when a form field is submitted. It passes the widget object and the form ID as arguments and expects a widget object as return value. It is available from version 2.5.0.

```php
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
