class Database
--------------

Provide methods to handle database communication.

### Description ###

**Definition:** `abstract class Database`

**Located in:** *system/libraries/Database.php*

**Class hierarchy:** *Database*



### Methods ###

- *public* [`getInstance`](Database/getInstance.md) – Instantiate a database driver object and return it (Factory)
- *public* [`__get`](Database/__get.md) – Return an object property
- *public* [`prepare`](Database/prepare.md) – Prepare a statement (return a Database_Statement object)
- *public* [`execute`](Database/execute.md) – Execute a query (return a Database_Result object)
- *public* [`executeUncached`](Database/executeUncached.md) – Execute a query and do not cache the result
- *public* [`query`](Database/query.md) – Execute a raw query (return a Database_Result object)
- *public* [`findInSet`](Database/findInSet.md) – Auto-generate a FIND_IN_SET() statement
- *public* [`listTables`](Database/listTables.md) – Return all tables of a database as array
- *public* [`tableExists`](Database/tableExists.md) – Determine if a particular database table exists
- *public* [`listFields`](Database/listFields.md) – Return all columns of a particular table as array
- *public* [`fieldExists`](Database/fieldExists.md) – Determine if a particular column exists
- *public* [`getFieldNames`](Database/getFieldNames.md) – Return the field names of a particular table as array
- *public* [`setDatabase`](Database/setDatabase.md) – Change the current database
- *public* [`beginTransaction`](Database/beginTransaction.md) – Begin a transaction
- *public* [`commitTransaction`](Database/commitTransaction.md) – Commit a transaction
- *public* [`rollbackTransaction`](Database/rollbackTransaction.md) – Rollback a transaction
- *public* [`lockTables`](Database/lockTables.md) – Lock one or more tables
- *public* [`unlockTables`](Database/unlockTables.md) – Unlock all tables
- *public* [`getSizeOf`](Database/getSizeOf.md) – Return the table size in bytes
- *public* [`getNextId`](Database/getNextId.md) – Return the next autoincrement ID of a table


### Properties ###

- *protected static* `$objInstance` - Current object instance (Singleton)
- *protected* `$resConnection` - Connection ID
- *protected* `$blnDisableAutocommit` - Disable autocommit
- *protected* `$arrCache` - Cache array
