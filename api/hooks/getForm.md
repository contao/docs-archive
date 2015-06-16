# getForm


The `getForm` allows to manipulate the generation of the forms.


## Parameters 

1. *Database_Result* `$objRow`

	Database result set from table `tl_form`.

2. *string* `$strBuffer`

	The generated form buffer.



## Return Values 

Return `$strBuffer` or your custom modification.


## Example 

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['getForm'][] = array('MyClass', 'myGetForm');

// MyClass.php
public function myGetForm(Database_Result $objRow, $strBuffer)
{
    if ($objRow->id == 2)
    {
        // Do something
    }

    return $strBuffer;
}
```


## More Information


### References

- [system/libraries/Controller.php](https://github.com/contao/core/blob/2.11.7/system/libraries/Controller.php#L561)


### See Also

- [getArticle](getArticle.md) – tiggered when an article is generated
- [getFrontendModule](getFrontendModule.md) – triggered when a frontend module is generated
