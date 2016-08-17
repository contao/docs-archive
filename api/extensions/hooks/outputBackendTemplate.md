# outputBackendTemplate

The `outputBackendTemplate` hook is triggered when a back end template is printed
to the screen. It passes the template content and the template name as arguments
and expects the template content as return value.

> #### primary:: Available   
> from Contao 2.6.0.


## Parameters

1. *string* `$strBuffer`

    Content of the rendered back end template.

2. *string* `$strTemplate`

    The template name (e.g. `be_main`) without file extension.


## Return Values

Return the original `$strBuffer` or return your custom modification.


## Example

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['outputBackendTemplate'][] = array('MyClass', 'myOutputBackendTemplate');

// MyClass.php
public function myOutputBackendTemplate($strBuffer, $strTemplate)
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

- [system/modules/core/classes/BackendTemplate.php](https://github.com/contao/core/blob/3.5.0/system/modules/core/classes/BackendTemplate.php#L110-L117)


### See also

- [outputFrontendTemplate](outputFrontendTemplate.md) - triggered when a front end template is printed to the screen.
- [parseBackendTemplate](parseBackendTemplate.md) - triggered when a back end template is parsed.
- [parseFrontendTemplate](parseFrontendTemplate.md) - triggered when a front end template is parsed.
