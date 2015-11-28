# outputFrontendTemplate

The `outputFrontendTemplate` hook is triggered when a front end template is
printed to the screen. It passes the template content and the template name as
arguments and expects the template content as return value. 

Note that `outputFrontendTemplate` is applied before the replacement of insert 
tags whereas the corresponding `modifyFrontendTemplate` is applied after insert 
tags have been replaced.

> **Tag** Available from version 2.6.0.


## Parameters

1. *string* `$strBuffer`

    Content of the rendered front end template.

2. *string* `$strTemplate`

    The template name (e.g. `fe_page`) without file extension.


## Return Values

Return the original `$strBuffer` or override with your custom modification.


## Example

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['outputFrontendTemplate'][] = array('MyClass', 'myOutputFrontendTemplate');

// MyClass.php
public function myOutputFrontendTemplate($strBuffer, $strTemplate)
{
    if ($strTemplate == 'fe_page')
    {
        // Modify output
    }

    return $strBuffer;
}
```


## More information


### References

- [system/modules/core/classes/FrontendTemplate.php](https://github.com/contao/core/blob/3.5.0/system/modules/core/classes/FrontendTemplate.php#L84-L91)


### See also

- [parseFrontendTemplate](parseFrontendTemplate.md) - triggered when a front end template is parsed.
- [modifyFrontendPage](modifyFrontendPage.md) - triggered when a front end page is printed to the screen.
- [outputBackendTemplate](outputBackendTemplate.md) - triggered when a back end template is printed to the screen.
- [parseBackendTemplate](parseBackendTemplate.md) - triggered when a back end template is parsed.
