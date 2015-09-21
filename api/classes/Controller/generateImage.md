
Controller :: generateImage
-------------------------------------------

Generate an image tag and return it as HTML string.


### Description ###

**Definition:** `protected function generateImage($src, $alt='', $attributes='')`

**Located in:** *system/libraries/Controller.php*

**Class hierarchy:** *[System](../System.md) > [Controller](../Controller.md)*


### Parameters ###

1. *string* `$src`

	The relative path to image.

2. *string* `$alt`

	The alternative text of the image.

3. *string* `$attributes`

	Additional image attributes.


### Return Values ###

The ```<img>``` HTML tag.


### Examples ###

1. Display an image with an alternative text

	```php
	<?php

	echo $this->generateImage('tl_files/music_academy/screenshot.jpg', 'Screenshot of Music Academy');
	```

### See also ###

- [`Controller::getImage`](getImage.md) – Get an image
- [`Controller::resizeImage`](resizeImage.md) – Resize or crop an image
- [`Controller::addImageToTemplate`](addImageToTemplate.md) – Add an image to the template
- [`getImage` hook](../../hooks/getImage.md) – triggered when a thumbnail is generated