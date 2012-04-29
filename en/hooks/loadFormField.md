loadFormField
-------------

The loadFormField hook is triggered when a form field is loaded. It passes the widget object, the form ID and the form data as arguments and expects a widget object as return value. It is available from version 2.5.0.

	// config.php
	$GLOBALS['TL_HOOKS']['loadFormField'][] = array('MyClass', 'myLoadFormField');
	 
	// MyClass.php
	public function myLoadFormField(Widget $objWidget, $strForm, $arrForm)
	{
	    $objWidget->class = 'myclass';
	    return $objWidget;
	}
