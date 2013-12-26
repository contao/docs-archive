
Controller :: addImageToTemplate
-------------------------------------------

Add an image to a template.


### Description ###

**Definition:** `protected function addImageToTemplate($objTemplate, $arrItem, $intMaxWidth=null, $strLightboxId=null)`

**Located in:** *system/libraries/Controller.php*

**Class hierarchy:** *[System](../System.md) > [Controller](../Controller.md)*


### Parameters ###

1. *object* `$objTemplate`

	A template object.

2. *array* `$arrItem`

	An associative array containing image data. *singleSRC* key is **necessary** here.

3. *integer* `$intMaxWidth`

	Maximum width of the image in pixels.

3. *string* `$strLightboxId`

	The name of lightbox ID.


### Examples ###

1. Add the image to a template

	```php
	<?php

	// ModuleCustom.php
	$arrImage = array('singleSRC'=>'tl_files/music_academy/screenshot.jpg', 'alt'=>'Screenshot of Music Academy');
	$this->addImageToTemplate($this->Template, $arrImage);

	// mod_custom.html5
	<?php if ($this->addImage): ?>
	<img src="<?php echo $this->src" alt="<?php echo $this->alt; ?>" />
	<?php endif; ?>
	```

### See Also ###

- [`Controller::getImage`](getImage.md) – Get an image
- [`Controller::resizeImage`](resizeImage.md) – Resize or crop an image
- [`Controller::generateImage`](generateImage.md) – Generate an image tag
- [`getImage` hook](../../hooks/getImage.md) – triggered when a thumbnail is generated
