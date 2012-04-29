loadDataContainer
-----------------

The loadDataContainer hook is triggered when a DCA file is loaded. It passes the file name as argument and does not expect a return value. It is available from version 2.8.2.

	// config.php
	$GLOBALS['TL_HOOKS']['loadDataContainer'][] = array('MyClass', 'myLoadDataContainer');
	 
	// MyClass.php
	public function myLoadDataContainer($strName)
	{
	    // Do something
	}
