# parseFrontendTemplate

The `parseFrontendTemplate` hook is triggered when a front end template is
parsed. It passes the template content and the template name as arguments
and expects the template content as return value.

> #### primary:: Available   
> from Contao 2.6.0.


## Parameters

1. *string* `$strBuffer`

    Content of the parsed front end template.

2. *string* `$strTemplate`

    The template name (e.g. `nav_default`) without file extension.


## Return Values

Return the original `$strBuffer` or override the template with your custom
modification.


## Example

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['parseFrontendTemplate'][] = array('MyClass', 'myParseFrontendTemplate');

// MyClass.php
public function myParseFrontendTemplate($strBuffer, $strTemplate)
{
    if ($strTemplate == 'ce_text')
    {
        // Modify output
    }

    return $strBuffer;
}
```


## More information


### References

- [system/modules/core/classes/FrontendTemplate.php](https://github.com/contao/core/blob/3.5.0/system/modules/core/classes/FrontendTemplate.php#L49-L56)


### See also

- [outputFrontendTemplate](outputFrontendTemplate.md) - triggered when a front end template is printed to the screen.
- [modifyFrontendPage](modifyFrontendPage.md) - triggered when a front end page is printed to the screen. 
- [outputBackendTemplate](outputBackendTemplate.md) - triggered when a back end template is printed to the screen.
- [parseBackendTemplate](parseBackendTemplate.md) - triggered when a back end template is parsed.
