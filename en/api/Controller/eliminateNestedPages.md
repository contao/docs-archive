
Controller :: eliminateNestedPages
-------------------------------------------

Take an array of paths and eliminate nested paths.


### Description ###

**Definition:** `protected function eliminateNestedPages($arrPages, $strTable=null, $blnSorting=false)`

**Located in:** *system/libraries/Controller.php*

**Class hierarchy:** *[System](../System.php) > [Controller](../Controller.php)*


### Return Values ###

An array of the not-nested pages.


### Parameters ###

1. *array* `$arrPages`

	Array containing the IDs of the pages.

2. *string* `$strTable`

	The table name to be executed. If none provided, *tl_page* will be used.

3. *boolean* `$blnSorting`

	If set to true, the pages will be sorted by *sorting* field.

### See Also ###

- [`Controller::eliminateNestedPath`](eliminateNestedPaths.md) – Eliminate nested paths in array

