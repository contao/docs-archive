# postDownload

The `postDownload` hook is triggered after a file has been downloaded with the
download/downloads content element. It passes the file name as argument and does
not expect a return value.

> **Tag** Available from version 2.4.6.


## Parameters

1. *string* $strFile

    The file which has been downloaded (relative path from `TL_ROOT`).


## Example

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['postDownload'][] = array('MyClass', 'myPostDownload');

// MyClass.php
public function myPostDownload($strFile)
{
    // Do something
}
```


## More information


### References

- [system/libraries/Controller.php](https://github.com/contao/core/blob/2.11.7/system/libraries/Controller.php#L2783)


### See also

- [postUpload](postUpload.md) - triggered after a user has uploaded one or more file in the back end
