# storeFormData


The `storeFormData` hook is triggered before a submitted form is stored to the database. It passes the result set and the form object and expects the result set as return value. Added in Contao 2.11.RC1


## Parameters 

1. *array* `$arrSet`

	The result set that will be written to the database table.

2. *Form* `$objForm`

	The form module instance.


## Return Values 

Return `$arrSet` or an array of key => values that should be written to the database.


## Example 

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['storeFormData'][] = array('MyClass', 'myStoreFormData');

// MyClass.php
public function myStoreFormData($arrSet, $objForm)
{
	$arrSet['member'] = 0;

	if (FE_USER_LOGGED_IN && $this->Database->fieldExists('member', $objForm->targetTable))
	{
		// Also store the member ID who submitted the form
		$arrSet['member'] = FrontendUser::getInstance()->id;
	}

	return $arrSet;
}
```


## More Information


### References

- [system/modules/frontend/Form.php](https://github.com/contao/core/blob/2.11.7/system/modules/frontend/Form.php#L438)


### See Also

- [processFormData](processFormData.md) – triggered after a form has been submitted
- [getForm](getForm.md) – manipulate the generation of the forms
- [loadFormField](loadFormField.md) – triggered when a form field is loaded
- [validateFormField](validateFormField.md) – triggered when a form field is submitted
