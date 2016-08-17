# isVisibleElement

The `isVisibleElement` hook is triggered when checking if an element should be
visible in the front end or not. An "element" in this case means either an article,
a front end module or a content element. In contrast to the other three hooks
`getArticle`, `getFrontendModule` and `getContentElement` one can prevent generating
the complete markup. The hook passes the model of the instance and the current
visibility state as arguments and expects the new visibility state as return value.

> #### primary:: Available   
> from Contao 3.2.RC1.


## Parameters

1. *Database_Result* `$objElement`

    The database result from table `tl_article` or `tl_content` or `tl_module`.

2. *boolean* `$blnIsVisible`

    The current visibility state.


## Return Values

Add some custom checks and return `true`, if the element should be visible in the front end.
Return `false` if the element should not be visible in the front end.


## Example

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['isVisibleElement'][] = array('MyClass', 'myIsVisibleElement');

// MyClass.php
public function myIsVisibleElement($objElement, $blnIsVisible)
{
    if ($objElement instanceof ContentElement)
    {
        // Check if this content element can be shown
        if ($this->myElementCanBeShownInFrontend($objElement))
        {
            return true;
        }
    }

    // Otherwise we don't want to change the visibility state
    return $blnIsVisible;
}
```

## More information


### References

- [system/modules/core/library/Contao/Controller.php](https://github.com/contao/core/blob/3.5.0/system/modules/core/library/Contao/Controller.php#L316-L322)


### See also

- [getArticle](getArticle.md) - tiggered when an article is generated.
- [getFrontendModule](getFrontendModule.md) - triggered when a front end module is generated.
- [getContentElement](getContentElement.md) - triggered when a content element is generated.
