outputFrontendTemplate
----------------------

The `outputFrontendTemplate` hook is triggered when a front end template is printed to the screen. It passes the template content and the template name as arguments and expects the template content as return value. It is available from version 2.6.0.


### Parameters ###

1. *string* `$strContent`

	Content of the rendered frontend template.

2. *string* `$strTemplate`

	The template name (e.g. `fe_page`) without file extension.


### Example ###

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['outputFrontendTemplate'][] = array('MyClass', 'myOutputFrontendTemplate');

// MyClass.php
public function myOutputFrontendTemplate($strContent, $strTemplate)
{
    if ($strTemplate == 'fe_page')
    {
        // Modify output
    }

    return $strContent;
}
```


### See Also ###

- [parseFrontendTemplate](parseFrontendTemplate.md) - triggered when a front end template is parsed
- [outputBackendTemplate](outputBackendTemplate.md) - triggered when a back end template is printed to the screen
- [parseBackendTemplate](parseBackendTemplate.md) - triggered when a back end template is parsed
