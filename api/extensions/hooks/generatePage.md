# generatePage

The `generatePage` hook is triggered before the main layout (fe_page) is compiled.
It passes the page object, the layout object and a self-reference as arguments and
does not expect a return value.

> #### tag:: Version Information 
> Available from Contao version 2.8.0-RC1.


## Parameters

1. *Database_Result* `$objPage`

    The current page object (enriched from `Controller::getPageDetails`).

2. *Database_Result* `$objLayout`

    The active page layout applied for rendering the page.

3.	*PageRegular* `$objPageRegular`

    The current page type object.


## Example

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['generatePage'][] = array('MyClass', 'myGeneratePage');

// MyClass.php
public function myGeneratePage(Database_Result $objPage, Database_Result $objLayout, PageRegular $objPageRegular)
{
    // Do something
}
```


## More information


### References

- [system/modules/core/pages/PageRegular.php](https://github.com/contao/core/blob/3.5.0/system/modules/core/pages/PageRegular.php#L151-L158)
