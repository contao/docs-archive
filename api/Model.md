
class Model
-----------

Provide active record functionality.


### Description ###

**Definition:** `abstract class Model extends System`

**Located in:** *system/libraries/Model.php*

**Class hierarchy:** *[System](System.md) > Model*


### Methods ###

- *public* [`__set`](Model/__set.md) – Set an object property
- *public* [`__get`](Model/__get.md) – Return an object property
- *public* [`__isset`](Model/__isset.md) – Check whether a property is set
- *public* [`setData`](Model/setData.md) – Set the current record from an object or array
- *public* [`getData`](Model/getData.md) – Return the current record as associative array
- *public* [`getDatabaseResult`](Model/getDatabaseResult.md) – Return the database result object
- *public* [`setFromRow`](Model/setFromRow.md) – Set the current record from a database result row
- *public* [`findBy`](Model/findBy.md) – Find a record by its reference field and return true if it has been found
- *public* [`save`](Model/save.md) – Save the current record and return the number of affected rows or the last insert ID
- *public* [`delete`](Model/delete.md) – Delete the current record and return the number of affected rows
