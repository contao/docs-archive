
Controller :: prepareForWidget
-------------------------------------------

Convert a back end DCA so it can be used with the widget class.


### Description ###

**Definition:** `protected function prepareForWidget($arrData, $strName, $varValue=null, $strField='', $strTable='')`

**Located in:** *system/libraries/Controller.php*

**Class hierarchy:** *[System](../System.php) > [Controller](../Controller.php)*


### Parameters ###

1. *array* `$arrData`

	An associative array containing field data.

2. *string* `$strName`

	The name of the field.

3. *mixed* `$varValue`

	The current value of the field.

4. *string* `$strField`

	The default field label.

5. *string* `$strTable`

	The name of the table (used in back end only).


### Examples ###

1. Generate the e-mail input field

	```php
	<?php

	$arrField = array
	(
		'name' => 'email',
		'label' => 'Your e-mail',
		'eval' => array('required'=>true, 'rgxp'=>'email')
	);

	$objWidget = new FormTextField($arrField, $arrField['name']);
	$strHtml = $objWidget->generateLabel() . ' ' . $objWidget->generateWithError()
	```