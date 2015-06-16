# parseFrontendTemplate


The `parseFrontendTemplate` hook is triggered when a front end template is parsed. It passes the template content and the template name as arguments and expects the template content as return value. It is available from version 2.6.0.


## Parameters 

1. *string* `$strBuffer`

	Content of the parsed frontend template.

2. *string* `$strTemplate`

	The template name (e.g. `nav_default`) without file extension.


## Return Values 

Return the original `$strBuffer` or override the template with your custom modification.


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


## More Information


### References

- [system/modules/frontend/FrontendTemplate.php](https://github.com/contao/core/blob/2.11.7/system/modules/frontend/FrontendTemplate.php#L51)


### See Also

- [outputFrontendTemplate](outputFrontendTemplate.md) - triggered when a front end template is printed to the screen
- [outputBackendTemplate](outputBackendTemplate.md) - triggered when a back end template is printed to the screen
