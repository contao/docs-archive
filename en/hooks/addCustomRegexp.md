addCustomRegexp
---------------

The addCustomRegexp hook is triggered when an unknown regular expression is found. It passes the name of the regexp, the current value and the widget object as arguments and expects a boolean return value. It is available from version 2.6.2.

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
