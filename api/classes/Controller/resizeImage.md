
Controller :: resizeImage
----------------------

Resize or crop an image. **Note:** this will not create a new image, but resize an existing one!

### Description ###

**Definition:** `protected function resizeImage($image, $width, $height, $mode='')`

**Located in:** *system/libraries/Controller.php*

**Class hierarchy:** *[System](../System.md) > [Controller](../Controller.md)*


### Parameters ###

1. *string* `$image`

	Path to the image that should be resized (relative from Contao root).

2. *int* `$width`

	The target width. Enter 0 if you only want to specify the height.

3. *int* `$height`

	The target height. Enter 0 if you only want to specify the with.

4. *string* `$mode`

	Through the resize mode, you can define how the image should be cropped. Can be any of the following, if empty the default will be used.
	- **proportional** *(default)* – 
		Adjusts the larger value of height or width to fit the same ratio as the image's dimensions.
	- **crop** – 
		 For backwards compatibility, equals **center_center**.
	- **left_top** – 
		Crop image from the left top corner.
	- **center_top** – 
		Crop image from horizontal center and vertical top border.
	- **right_top** – 
		Crop image from right top corner.
	- **left_center**
		Crop image from horizontal left border and vertical center.
	- **center_center** – 
		Crop image from the center.
	- **right_center** – 
		Crop image from horizontal right border and vertical center.
	- **left_bottom** – 
		Crop image from left bottom corner.
	- **center_bottom** – 
		Crop image from horizontal center and vertical bottom border.
	- **right_bottom** – 
		Crop image from horizontal right and vertical bottom border.


### Return Values ###

A relative path of the resized image.


### Examples ###

1. Resize an image with default options. Passing no `$mode`, the crop is **proportional** and therefore the image will be 100px width (larger side) but not 100px height.

	```php
	<?php

	$strImage = $this->getImage('tl_files/music_academy/screenshot.jpg', 100, 100);
	echo $strImage;
	```
	> tl_files/music_academy/screenshot.jpg

	![100x100 crop from the center]
	(../../assets/api/Controller/getImage-1.jpg)

2. Resize an image from right top corner. The smaller side will be adjusted, the larger will be cropped.

	```php
	<?php

	$strImage = $this->getImage('tl_files/music_academy/screenshot.jpg', 100, 100, 'right_top');
	echo $strImage;
	```
	> tl_files/music_academy/screenshot.jpg

	![100x100 crop from top right corner]
	(../../assets/api/Controller/getImage-2.jpg)

### See also ###

- [`Controller::getImage`](getImage.md) – Get an image
- [`Controller::generateImage`](generateImage.md) – Generate an image tag
- [`Controller::addImageToTemplate`](addImageToTemplate.md) – Add an image to the template
- [`getImage` hook](../../hooks/getImage.md) – triggered when a thumbnail is generated
