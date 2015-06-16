# parseTemplate


The `parseTemplate` hook is triggered before parsing a template. It passes the template object and does not expect a return value.


## Parameters 

1. *Template* `$objTemplate`

	The frontend or backend template instance.


## Example 

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


## More Information


### References

- [system/libraries/Template.php](https://github.com/contao/core/blob/2.11.7/system/libraries/Template.php#L235)


### See Also

- [parseBackendTemplate](parseBackendTemplate.md) – triggered when a back end template is parsed
