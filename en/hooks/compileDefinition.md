compileDefinition
-----------------

The compileDefinition hook is triggered when a format definition of a style sheet is written. It passes the configuration array as argument and expects a string as return value. It is available from version 2.9.4.

	// config.php
	$GLOBALS['TL_HOOKS']['compileDefinition'][] = array('MyClass', 'myCompileDefinition');
	 
	// MyClass.php
	public function myCompileDefinition($arrRow)
	{
	    if (isset($arrRow['border-radius']))
	    {
	        return "\nborder-radius:" . $arrRow['border-radius'] . ";";
	    }
	 
	    return '';
	}