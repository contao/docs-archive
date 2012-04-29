reviseTable
-----------

The reviseTable hook is triggered when Contao removes orphan records from a table. It passes the name of the current table, the IDs of all new records, the name of the parent table and the names of all child tables as arguments and does expect a boolean return value (returning true will cause the current page to be reloaded). It is available from version 2.6.4.

	// config.php
	$GLOBALS['TL_HOOKS']['reviseTable'][] = array('MyClass', 'myReviseTable');
	 
	// MyClass.php
	public function myReviseTable($table, $new_records, $parent_table, $child_tables)
	{
	    // Do something
	}
