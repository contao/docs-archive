parseTemplate
-------------

The `parseTemplate` hook is triggered before parsing a template. It passes the template object and does not expect a return value.


### Parameters ###

1. *Template* `$objTemplate`

	The frontend or backend template instance.


### Example ###

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['parseTemplate'][] = array('MyClass', 'myParseTemplate');

// MyClass.php
public function myParseTemplate($objTemplate)
{
	if ($objTemplate->getName() == 'fe_page')
	{
		// Do something
	}
}
```


### See Also ###

- [parseBackendTemplate](parseBackendTemplate.md) – triggered when a back end template is parsed
- [parseFrontendTemplate](parseFrontendTemplate.md) – triggered when a front end template is parsed
