# outputBackendTemplate


The `outputBackendTemplate` hook is triggered when a back end template is printed to the screen. It passes the template content and the template name as arguments and expects the template content as return value. It is available from version 2.6.0.


## Parameters 

1. *string* `$strBuffer`

	Content of the rendered backend template.

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


## More Information


### References

- [system/modules/backend/BackendTemplate.php](https://github.com/contao/core/blob/2.11.7/system/modules/backend/BackendTemplate.php#L146)


### See Also

- [outputFrontendTemplate](outputFrontendTemplate.md) - triggered when a front end template is printed to the screen
- [parseBackendTemplate](parseBackendTemplate.md) - triggered when a back end template is parsed
- [parseFrontendTemplate](parseFrontendTemplate.md) - triggered when a front end template is parsed
