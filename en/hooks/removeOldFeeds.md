removeOldFeeds
--------------

The `removeOldFeeds` hook is triggered when old XML files are being removed from the Contao root directory. It does not pass an argument and expects an array of file names to preserve as return value. It is available from version 2.5.8.


### Return Values ###

Return an array of XML file names (**do not include** file extension!) that **must not** be removed from the root directory. Return an empty array if you have nothing to keep.


### Example ###

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['removeOldFeeds'][] = array('MyClass', 'myRemoveOldFeeds');

// MyClass.php
public function myRemoveOldFeeds()
{
    return array('custom.xml');
}
```


### See Also ###

- [reviseTable](reviseTable.md) – riggered when Contao removes orphan records from a table