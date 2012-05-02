parseFrontendTemplate
---------------------

The `parseFrontendTemplate` hook is triggered when a front end template is parsed. It passes the template content and the template name as arguments and expects the template content as return value. It is available from version 2.6.0.


### Example ###

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['parseFrontendTemplate'][] = array('MyClass', 'myParseFrontendTemplate');

// MyClass.php
public function myParseFrontendTemplate($strContent, $strTemplate)
{
    if ($strTemplate == 'ce_text')
    {
        // Modify output
    }

    return $strContent;
}
```
