
Controller :: getImage
----------------------

Resize an image.

### Description ###

**Definition:** `protected function getImage($image, $width, $height, $mode='', $target=null)`

**Located in:** *system/libraries/Controller.php*

**Class hierarchy:** *[System](../System.php) > [Controller](../Controller.php)*


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

5. *string* `$target`

	Target path to store the resized image. By default it will be stored in system/html/ with a unique file name. You should not change this in most cases.


### Examples ###

1. Resize an image with default options. Passing no `$mode`, the crop is **proportional** and therefore the image will be 100px width (larger side) but not 100px height.

	```php
	<?php

	$strImage = $this->getImage('tl_files/music_academy/screenshot.jpg', 100, 100);
	echo $strImage;
	```
	> system/html/screenshot-b5775910.jpg

	![100x100 crop from the center]
	(../../assets/api/Controller/getImage-1.jpg)

2. Resize an image from right top corner. The smaller side will be adjusted, the larger will be cropped.

	```php
	<?php

	$strImage = $this->getImage('tl_files/music_academy/screenshot.jpg', 100, 100, 'right_top');
	echo $strImage;
	```
	> system/html/screenshot-66a7cd8c.jpg

	![100x100 crop from top right corner]
	(https://github.com/contao/docs/raw/2.11/en/assets/api/Controller/getImage-2.jpg)

### See Also ###

- [`Controller::resizeImage`](resizeImage.md) – Resize or crop an image
- [`getImage` hook](../../hooks/getImage.md) – triggered when a thumbnail is generated
