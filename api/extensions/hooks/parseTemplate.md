# parseTemplate

The `parseTemplate` hook is triggered before parsing a template. It passes the
template object and does not expect a return value.


## Parameters

1. *Template* `$objTemplate`

    The front end or back end template instance.


## Example

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['parseTemplate'][] = array('MyClass', 'myParseTemplate');

// MyClass.php
public function myParseTemplate($objTemplate)
{
    if ($objTemplate->getName() == 'fe_page')
    {
        // Do something
    }
}
```


## More information


### References

- [system/modules/core/library/Contao/Template.php](https://github.com/contao/core/blob/3.5.0/system/modules/core/library/Contao/Template.php#L241-L248)


### See also

- [parseBackendTemplate](parseBackendTemplate.md) – triggered when a back end template is parsed.
- [parseFrontendTemplate](parseFrontendTemplate.md) – triggered when a front end template is parsed.
