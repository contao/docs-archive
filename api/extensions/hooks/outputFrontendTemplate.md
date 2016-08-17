# outputFrontendTemplate

The `outputFrontendTemplate` hook is triggered when a front end template is
printed to the screen. It passes the template content and the template name as
arguments and expects the template content as return value. 

> #### info:: Note 
> This hook is applied before the replacement of insert tags 
> whereas the corresponding [`modifyFrontendTemplate`][1] is applied after 
> insert tags have been replaced.

<!-- blockquote break -->

> #### primary:: Available   
> from Contao 2.6.0.


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
$GLOBALS['TL_HOOKS']['outputFrontendTemplate'][] = array('MyClass', 'myOutputFrontendTemplate');

// MyClass.php
public function myOutputFrontendTemplate($buffer, $templateName)
{
    if ('fe_page' === $templateName) {
        // Modify output
    }

    return $buffer;
}
```


## More information


### References

- [system/modules/core/classes/FrontendTemplate.php](https://github.com/contao/core/blob/3.5.0/system/modules/core/classes/FrontendTemplate.php#L84-L91)


### See also

- [parseFrontendTemplate](parseFrontendTemplate.md) - triggered when a front end template is parsed.
- [modifyFrontendPage][1] - triggered when a front end page is printed to the screen.
- [outputBackendTemplate](outputBackendTemplate.md) - triggered when a back end template is printed to the screen.
- [parseBackendTemplate](parseBackendTemplate.md) - triggered when a back end template is parsed.


[1]: modifyFrontendPage.md
