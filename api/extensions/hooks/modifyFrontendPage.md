# modifyFrontendPage

The `modifyFrontendPage` hook is triggered when a front end template is
printed to the screen. It passes the template content and the template name as
arguments and expects the template content as return value.

> #### info:: Note 
> This hook is applied after insert tags have been
> replaced. If you want to apply your logic before the replacement of
> insert tags, use the [`outputFrontendTemplate`][1] hook instead.

<!-- blockquote break -->

> #### primary:: Available   
> from Contao 3.1.beta1.


## Parameters

1. *string* `$buffer`

    Content of the rendered front end template.

2. *string* `$templateName`

    The template name (e.g. `fe_page`) without file extension.


## Return Values

Return the original `$buffer` or override with your custom modification.


## Example

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['modifyFrontendPage'][] = array('MyClass', 'myModifyFrontendPage');

// MyClass.php
public function myModifyFrontendPage($buffer, $templateName)
{
    if ('fe_page' === $templateName) {
        // Modify output
    }

    return $strBuffer;
}
```


## More information


### References

- [system/modules/core/classes/FrontendTemplate.php](https://github.com/contao/core/blob/3.5.0/system/modules/core/classes/FrontendTemplate.php#L105-L112)
- [system/modules/core/controllers/FrontendIndex.php](https://github.com/contao/core/blob/3.5.0/system/modules/core/controllers/FrontendIndex.php#457-L464)


### See also

- [parseFrontendTemplate](parseFrontendTemplate.md) - triggered when a front end template is parsed.
- [outputFrontendTemplate][1] - triggered when a front end template is printed to the screen.
- [outputBackendTemplate](outputBackendTemplate.md) - triggered when a back end template is printed to the screen.
- [parseBackendTemplate](parseBackendTemplate.md) - triggered when a back end template is parsed.



[1]: outputFrontendTemplate.md
