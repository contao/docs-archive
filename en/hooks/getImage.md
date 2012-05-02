getImage
--------

The `getImage` hook is triggered when a thumbnail is generated and allows you to add a custom routine. It passes the path, the width and height, the mode, the cache name and the file object as arguments and expects a path as return value. It is available from version 2.8.RC1.


### Example ###

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['getImage'][] = array('MyClass', 'myGetImage');

// MyClass.php
public function myGetImage($image, $width, $height, $mode, $strCacheName, $objFile)
{
    return MyImage::generateThumbnail($image, $widht, $height, $mode);
}
```
