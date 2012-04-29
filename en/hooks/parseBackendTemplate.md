parseBackendTemplate
--------------------

The parseBackendTemplate hook is triggered when a back end template is parsed. It passes the template content and the template name as arguments and expects the template content as return value. It is available from version 2.6.0.

	// config.php
	$GLOBALS['TL_HOOKS']['parseBackendTemplate'][] = array('MyClass', 'myParseBackendTemplate');
	 
	// MyClass.php
	public function myParseBackendTemplate($strContent, $strTemplate)
	{
	    if ($strTemplate == 'be_main')
	    {
	        // Modify output
	    }
	 
	    return $strContent;
	}
