closeAccount
------------

The closeAccount hook is triggered when a user closes his account. It passes the user ID, the operation mode and the module as arguments and does not expect a return value. It is available from version 2.8.0.

	// config.php
	$GLOBALS['TL_HOOKS']['closeAccount'][] = array('MyClass', 'myCloseAccount');
 
	// MyClass.php
	public function myCloseAccount($intId, $strMode, $objModule)
	{
	    if ($strMode == 'close_delete')
	    {
	        // Do something
	    }
	}
