postUpload
----------

The `postUpload` hook is triggered after a user has uploaded one or more file in the back end. It passes an array of filenames as argument and does not expect a return value. It is available from version 2.6.4.


### Parameters ###

1. *array* `$arrFiles`

	List of files that have been uploaded. The file paths are relative to the Contao root directory.


### Example ###

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['postUpload'][] = array('MyClass', 'myPostUpload');

// MyClass.php
public function myPostUpload($arrFiles)
{
    // Do something
}
```


### See Also ###

- [postDownload](postDownload.md) - triggered after a file has been downloaded with the download/downloads content element
