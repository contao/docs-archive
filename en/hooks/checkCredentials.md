checkCredentials
----------------

The checkCredentials hook is triggered when a login attempt fails due to a wrong password. It passes the username and password as well as the user object as arguments and expects a boolean return value. It is available from version 2.6.0.

	// config.php
	$GLOBALS['TL_HOOKS']['checkCredentials'][] = array('MyClass', 'myCheckCredentials');
 
	// MyClass.php
	public function myCheckCredentials($strUsername, $strPassword, User $objUser)
	{
	    // Check against a global database
	    if ($this->checkGlobalDbFor($strUsername, $strPassword))
	    {
	        return true;
	    }
	 
	    return false;
	}