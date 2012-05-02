outputBackendTemplate
---------------------

The `outputBackendTemplate` hook is triggered when a back end template is printed to the screen. It passes the template content and the template name as arguments and expects the template content as return value. It is available from version 2.6.0.


### Example ###

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['outputBackendTemplate'][] = array('MyClass', 'myOutputBackendTemplate');

// MyClass.php
public function myOutputBackendTemplate($strContent, $strTemplate)
{
    if ($strTemplate == 'be_main')
    {
        // Modify output
    }

    return $strContent;
}
```
