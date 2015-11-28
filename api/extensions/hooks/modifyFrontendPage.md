# modifyFrontendPage

The `modifyFrontendPage` hook is triggered when a front end template is
printed to the screen. It passes the template content and the template name as
arguments and expects the template content as return value.

Note that `modifyFrontendTemplate` is applied after insert tags have been 
replaced. If you want to apply your logic before the replacement of
 insert tags use `outputFrontendTemplate` instead.

> **Tag** Available from version 3.1.beta1.


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
$GLOBALS['TL_HOOKS']['modifyFrontendPage'][] = array('MyClass', 'myModifyFrontendPage');

// MyClass.php
public function myModifyFrontendPage($strBuffer, $strTemplate)
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

- [system/modules/core/classes/FrontendTemplate.php](https://github.com/contao/core/blob/3.5.0/system/modules/core/classes/FrontendTemplate.php#L105-L112)


### See also

- [parseFrontendTemplate](parseFrontendTemplate.md) - triggered when a front end template is parsed.
- [outputFrontendTemplate](outputFrontendTemplate.md) - triggered when a front end template is printed to the screen.
- [outputBackendTemplate](outputBackendTemplate.md) - triggered when a back end template is printed to the screen.
- [parseBackendTemplate](parseBackendTemplate.md) - triggered when a back end template is parsed.