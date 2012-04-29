postLogout
----------

The postLogout hook is triggered after a user has logged out from the front end. It passes the user object as argument and does not expect a return value. It is available from version 2.4.3.

	// config.php
	$GLOBALS['TL_HOOKS']['postLogout'][] = array('MyClass', 'myPostLogout');
	 
	// MyClass.php
	public function myPostLogout(FrontendUser $objUser)
	{
	    // Do something
	}
