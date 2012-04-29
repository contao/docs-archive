postDownload
------------

The postDownload hook is triggered after a file has been downloaded with the download(s) element. It passes the file name as argument and does not expect a return value. It is available from version 2.4.6.

	// config.php
	$GLOBALS['TL_HOOKS']['postDownload'][] = array('MyClass', 'myPostDownload');
	 
	// MyClass.php
	public function myPostDownload($strFile)
	{
	    // Do something
	}
