addCustomRegexp
---------------

The ```addCustomRegexp``` hook is triggered when an unknown regular expression is found. It passes the name of the regexp, the current value and the widget object as arguments and expects a boolean return value. It is available from version 2.6.2.


### Parameters ###

- *string* ```$strRegexp```

	The unknown regular expression string

- *mixed* ```$varValue```

	The input value to be validated

- *Widget* ```$objWidget```

	Form widget which is handling this input value.  
	Use the widget's properties to retrieve information about the field configuration.


### Example ###

```php
// config.php
$GLOBALS['TL_HOOKS']['addCustomRegexp'][] = array('MyClass', 'myAddCustomRegexp');
 
// MyClass.php
public function myAddCustomRegexp($strRegexp, $varValue, Widget $objWidget)
{
    if ($strRegexp == 'postal')
    {
        if (!preg_match('/^0-9{4,6}$/', $varValue))
        {
            $objWidget->addError('Field ' . $objWidget->label . ' should be a postal code.');
        }
 
        return true;
    }
 
    return false;
}
``` 


### See Also ###

- [replaceInsertTags](hooks/replaceInsertTags.md) - triggered when an unknown insert tag is found