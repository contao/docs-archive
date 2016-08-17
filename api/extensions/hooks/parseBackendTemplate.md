# parseBackendTemplate

The `parseBackendTemplate` hook is triggered when a back end template is parsed.
It passes the template content and the template name as arguments and expects
the template content as return value.

> #### primary:: Available   
> from Contao 2.6.0.


## Parameters

1. *string* `$strBuffer`

    Content of the parsed back end template.

2. *string* `$strTemplate`

    The template name (e.g. `be_widget`) without file extension.


## Return Values

Return the original `$strBuffer` or override with your custom modification.

## Example

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['parseBackendTemplate'][] = array('MyClass', 'myParseBackendTemplate');

// MyClass.php
public function myParseBackendTemplate($strBuffer, $strTemplate)
{
    if ($strTemplate == 'be_main')
    {
        // Modify output
    }

    return $strBuffer;
}
```


## More information


### References

- [system/modules/core/classes/BackendTemplate.php](https://github.com/contao/core/blob/3.5.0/system/modules/core/classes/BackendTemplate.php#L37-L44)


### See also

- [parseFrontendTemplate](parseFrontendTemplate.md) - triggered when a front end template is parsed.
- [outputFrontendTemplate](outputFrontendTemplate.md) - triggered when a front end template is printed to the screen.
- [outputBackendTemplate](outputBackendTemplate.md) - triggered when a back end template is printed to the screen.
