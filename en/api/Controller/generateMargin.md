
Controller :: generateMargin
-------------------------------------------

Take an array of four margin values and the current unit and compile the margin style definition.


### Description ###

**Definition:** `protected function generateMargin($arrValues, $strType='margin')`

**Located in:** *system/libraries/Controller.php*

**Class hierarchy:** *[System](../System.php) > [Controller](../Controller.php)*


### Parameters ###

1. *array* `$arrValues`

	An associative array that contains four margin values: *top, right, bottom, left*; and the *unit* name.

2. *string* `$strType`

	The CSS property name.


### Return Values ###

The CSS definition.


### Examples ###

1. Generate a 20px margin CSS definition

	```php
	<?php

	$arrMargin = array('top'=>20, 'right'=>20, 'bottom'=>20, 'left'=>20, 'unit'=>'px');
	echo $this->generateMargin($arrMargin);
	```
	> margin:20px;

1. Generate a 5/10/15/20px padding CSS definition

	```php
	<?php

	$arrPadding = array('top'=>5, 'right'=>10, 'bottom'=>15, 'left'=>20, 'unit'=>'px');
	echo $this->generateMargin($arrPadding, 'padding');
	```
	> padding:5px 10px 15px 20px;

