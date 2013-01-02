
class Files
-----------

Provide methods to modify files and folders.


### Description ###

**Definition:** `class File`

**Located in:** *system/libraries/Files.php*

**Class hierarchy:** *Files*


### Methods ###

- *public* [`getInstance`](Files/getInstance.md) – Instantiate a files driver object and return it (Factory)
- *public* [`mkdir`](Files/mkdir.md) – Create a directory
- *public* [`rmdir`](Files/rmdir.md) – Remove a directory
- *public* [`rrdir`](Files/rrdir.md) – Recursively remove a directory
- *public* [`fopen`](Files/fopen.md) – Open a file and return the handle
- *public* [`fputs`](Files/fputs.md) – Write content to a file
- *public* [`fclose`](Files/fclose.md) – Close a file
- *public* [`rename`](Files/rename.md) – Rename a file or folder
- *public* [`copy`](Files/copy.md) – Copy a file or folder
- *public* [`delete`](Files/delete.md) – Delete a file
- *public* [`is_writeable`](Files/is_writeable.md) – Check whether a file is writeable
- *public* [`move_uploaded_file`](Files/move_uploaded_file.md) – Move an uploaded file to another folder


### Properties ###

- *protected static* `$objInstance` - Current object instance (Singleton)
