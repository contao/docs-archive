
Email :: __get
-------------------------------------------

Return an object property.


### Description ###

**Definition:** `public function __get($strKey)`

**Located in:** *system/libraries/Email*

**Class hierarchy:** *[System](../System.php) > [Email](../Email)*


### Parameters ###

1. *string* `$strKey`

	Name of the property to be returned. Return null, if property is not found.	
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
	- **failures** – 
		The array of sending failures.
		

### Return Values ###

Mixed values.

