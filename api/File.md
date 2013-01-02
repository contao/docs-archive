
class File
----------

Provide methods to handle files.


### Description ###

**Definition:** `class File extends System`

**Located in:** *system/libraries/File.php*

**Class hierarchy:** *[System](System.md) > File*


### Methods ###

- *public* [`__construct`](File/__construct.md) – Check whether a file exists
- *public* [`__get`](File/__get.md) – Return an object property
- *public* [`truncate`](File/truncate.md) – Truncate the file
- *public* [`write`](File/write.md) – Write data to the file
- *public* [`append`](File/append.md) – Append data to the file
- *public* [`delete`](File/delete.md) – Delete the file
- *public* [`chmod`](File/chmod.md) – Set the file permissions
- *public* [`close`](File/close.md) – Close the file handle
- *public* [`getContent`](File/getContent.md) – Return file content as string
- *public* [`getContentAsArray`](File/getContentAsArray.md) – Return file content as array
- *public* [`renameTo`](File/renameTo.md) – Rename the file
- *public* [`copyTo`](File/copyTo.md) – Copy the file


### Properties ###

- *protected* `$resFile` - File handle
- *protected* `$strFile` - File name
- *protected* `$arrPathinfo` - Pathinfo
- *protected* `$arrImageSize` - Image size

