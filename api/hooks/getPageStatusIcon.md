# getPageStatusIcon #

The `getPageStatusIcon` hook is triggered when the appropriate page status icon is calculated. It passes the database result object and the filename of the current icon as arguments and expects a file name as return value. 
> **tag** It is available from version 3.5.0.


## Parameters ##

1. *Database_Result* `$objPage`

	Database result set from table `tl_page`.

2. *string* `$image`

	The file name of the default status icon calculated by Contao.


## Return Value ##

You can specify a new image to be displayed in the backend by returning a filename.


## Example ##

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['myGetPageStatusIcon'][] = array('MyClass', 'myGetPageStatusIcon');

// MyClass.php
public function myGetPageStatusIcon(Database_Result $objPage, $image)
{
    return 'custom_icon.gif';
}
```


## More Information ##


### References ###

- [system/libraries/Controller.php](https://github.com/contao/core/blob/master/system/modules/core/library/Contao/Controller.php#L608)