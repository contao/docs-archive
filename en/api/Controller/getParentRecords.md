
Controller :: getParentRecords
-------------------------------------------

Return the IDs of all child records of a particular record.


### Description ###

**Definition:** `protected function getParentRecords($strTable, $intId)`

**Located in:** *system/libraries/Controller.php*

**Class hierarchy:** *[System](../System.php) > [Controller](../Controller.php)*


### Return Values ###

An array containing IDs of child records of the specified parent record.


### Parameters ###

1. *string* `$strTable`

	A name of the table to be executed.

2. *integer* `$intId`

	The numberic ID of parent record.
	

### See Also ###

- [`Controller::getChildRecords`](getChildRecords.md) – Get the child records


