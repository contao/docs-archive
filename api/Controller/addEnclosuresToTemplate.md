
Controller :: addEnclosuresToTemplate
-------------------------------------------

Add enclosures to a template.


### Description ###

**Definition:** `protected function addEnclosuresToTemplate($objTemplate, $arrItem)`

**Located in:** *system/libraries/Controller.php*

**Class hierarchy:** *[System](../System.md) > [Controller](../Controller.md)*


### Parameters ###

1. *object* `$objTemplate`

	A template object.

2. *array* `$arrItem`

	An array containing file paths.


### Examples ###

1. Add the image to a template

	```php
	<?php

	// ModuleCustom.php
	$arrItems = array('tl_files/downloads/file1.zip', 'tl_files/downloads/file1.zip');
	$this->addEnclosuresToTemplate($this->Template, $arrItems);

	// mod_custom.html5
	<?php if ($this->enclosure): ?>
	<?php foreach ($this->enclosure as $enclosure): ?>
	<a href="<?php echo $enclosure['href']; ?>"><?php echo $enclosure['title']; ?></a>
	<?php endforeach; ?>
	<?php endif; ?>
	```

