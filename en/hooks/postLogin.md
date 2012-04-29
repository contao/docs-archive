postLogin
---------

The postLogin hook is triggered after a user has logged into the front end. It passes the user object as argument and does not expect a return value. It is available from version 2.4.3.

	// config.php
	$GLOBALS['TL_HOOKS']['postLogin'][] = array('MyClass', 'myPostLogin');
	 
	// MyClass.php
	public function myPostLogin(FrontendUser $objUser)
	{
	    // Do something
	}
