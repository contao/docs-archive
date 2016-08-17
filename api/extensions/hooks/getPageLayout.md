# getPageLayout

The `getPageLayout` hook is triggered when a regular page is generated.
It can be used to modify the page or layout object.
It passes the page object, the layout object and the page type instance as arguments
and does not expect a return value.

> #### primary:: Available   
> from Contao 3.1.0.


## Parameters

1. *object* `$objPage`

	The page.

2. *object* `$objLayout`

	The layout of the page.

3. *object* `$objPty`

	 The page type instance (`PageRegular`).


## Example

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['getPageLayout'][] = array('MyClass', 'myGetPageLayout');

// MyClass.php
public function myGetPageLayout($objPage, $objLayout, $objPty)
{
    // modify the page or layout object

}
```


## More Information


### References

- [system/modules/core/pages/PageRegular.php](https://github.com/contao/core/blob/support/3.2/system/modules/core/pages/PageRegular.php#L46)
