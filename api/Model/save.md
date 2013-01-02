
Model :: save
-------------------------------------------

Save the current record and return the number of affected rows or the last insert ID.


### Description ###

**Definition:** `public function save($blnForceInsert=false)`

**Located in:** *system/libraries/Model.php*

**Class hierarchy:** *[System](../System.md) > [Model](../Model.md)*


### Parameters ###

1. *boolean* `$blnForceInsert`

	If true, the record will be inserted even if it already exists. Defaults to false.


### Return Values ###

Number of affected rows or the last insert ID.
