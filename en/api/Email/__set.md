
Email :: __set
-------------------------------------------

Set an object property.


### Description ###

**Definition:** `public function __set($strKey, $varValue)`

**Located in:** *system/libraries/Email.php*

**Class hierarchy:** *[System](../System.md) > [Email](../Email.md)*


### Parameters ###

1. *string* `$strKey`

	Name of the property to be set.
	- **subject** -
		The e-mail subject.
	- **text** –
		The e-mail plain text content.
	- **html** –
		The e-mail HTML content.
	- **from** –
		The recipient's e-mail address.
	- **fromName** –
		The recipient's name.
	- **priority** –
		The e-mail priority (1 - highest, 5 - lowest).
	- **charset** –
		The e-mail character set.
	- **imageDir** –
		The e-mail image directory.
	- **embedImages** –
		Whether to embed images or not.
	- **logFile** –
		The file name where e-mail logs are stored.


2. *mixed* `$varValue`

	The value to be set.

