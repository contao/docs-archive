outputFrontendTemplate
----------------------

The ```outputFrontendTemplate``` hook is triggered when a front end template is printed to the screen. It passes the template content and the template name as arguments and expects the template content as return value. It is available from version 2.6.0.


### Example ###

```php
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
