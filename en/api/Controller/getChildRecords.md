
Controller :: getChildRecords
-------------------------------------------

Return the IDs of all child records of a particular record.


### Description ###

**Definition:** `protected function getChildRecords($arrParentIds, $strTable, $blnSorting=false, $arrReturn=array())`

**Located in:** *system/libraries/Controller.php*

**Class hierarchy:** *[System](../System.php) > [Controller](../Controller.php)*


### Parameters ###

1. *array* `$arrParentIds`

	An array of the parent IDs.

2. *string* `$strTable`

	A name of the table to be executed.

3. *boolean* `$blnSorting`

	If set to true, the *sorting* field will be used to sort the output.

4. *array* `$arrReturn`

	An array to be merged with the result.


