processFormData
---------------

The processFormData hook is triggered after a form has been submitted. It passes the form data array, the Data Container Array and the files array as arguments and does not expect a return value. It is available from version 2.4.4.

	// config.php
	$GLOBALS['TL_HOOKS']['processFormData'][] = array('MyClass', 'myProcessFormData');
	 
	// MyClass.php
	public function myProcessFormData($arrPost, $arrForm, $arrFiles)
	{
	    // Do something
	}
