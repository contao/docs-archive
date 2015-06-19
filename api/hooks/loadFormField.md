# loadFormField


The `loadFormField` hook is triggered when a form field is loaded. It passes the widget object, the form ID and the form data as arguments and expects a widget object as return value. It is available from version 2.5.0.


## Parameters 

1. *Widget* `$objWidget`

	Instance of the current frontend widget.

2. *string* `$strForm`

	Alias of the current form.

3. *array* `$arrForm`

	The form configuration, a tl_form record.


## Return Values 

Return the `$objWidget` instance. You can override it's settings or even create your own widget instead.


## Example 

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['loadFormField'][] = array('MyClass', 'myLoadFormField');

// MyClass.php
public function myLoadFormField(Widget $objWidget, $strForm, $arrForm)
{
    $objWidget->class = 'myclass';
    return $objWidget;
}
```


## More Information


### References

- [system/modules/frontend/Form.php](https://github.com/contao/core/blob/2.11.7/system/modules/frontend/Form.php#L157)


### See Also

- [validateFormField](validateFormField.md) - triggered when a form field is submitted
- [processFormData](processFormData.md) - triggered after a form has been submitted
