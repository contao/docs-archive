# getPageStatusIcon

The `getPageStatusIcon` hook is triggered when the appropriate page status icon 
is calculated. It passes the database result object and the file name of the 
current icon as arguments and expects a file name as return value. 

> #### primary:: Available   
> from Contao 3.5.0.


## Parameters

1. *Database_Result* `$objPage`

	Database result set from table `tl_page`.

2. *string* `$image`

	The file name of the default status icon calculated by Contao.


## Return Value

You must always return a file name, which can be either a custom file name or 
the unchanged second parameter. 


## Example

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['myGetPageStatusIcon'][] = array('MyClass', 'myGetPageStatusIcon');

// MyClass.php
public function myGetPageStatusIcon(Database_Result $objPage, $image)
{
    if ($objPage->type == 'my_page')
    {
        return 'path/to/custom_icon.gif';
    }

    return $image;

}
```


## More Information


### Reference

- [system/libraries/Controller.php](https://github.com/contao/core/blob/3.5.0/system/modules/core/library/Contao/Controller.php#L608)