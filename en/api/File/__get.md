
File :: __get
-------------------------------------------

Return an object property.


### Description ###

**Definition:** `public function __get($strKey)`

**Located in:** *system/libraries/File.php*

**Class hierarchy:** *[System](../System.md) > [File](../File.md)*


### Parameters ###

1. *string* `$strKey`

	Name of the property to be returned. Return null, if property is not found.
	- **size, filesize** -
		The file size.
	- **dirname, basename** –
		The basename of the file.
	- **extension** –
		The extension of the file.
	- **filename** –
		The full file name.
	- **mime** –
		The file mime type.
	- **ctime** –
		The inode change time of file.
	- **mtime** –
		The time of file modification.
	- **atime** –
		The last access time of file.
	- **icon** –
		The file type icon.
	- **value** –
		The file name.
	- **width** –
		The width of the image.
	- **height** –
		The height of the image.
	- **isGdImage** –
		True if the image is a GD image, false otherwise.
	- **handle** –
		The image resource handle.


### Return Values ###

Mixed values.

