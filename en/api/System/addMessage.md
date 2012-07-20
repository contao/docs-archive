
System :: addMessage
-------------------------------------------

Add a message.


### Description ###

**Definition:** `protected function addMessage($strMessage, $strType)`

**Located in:** *system/libraries/System*

**Class hierarchy:** *[System](../System.md)*

**Throws:** *Exception*


### Parameters ###

1. *string* `$strMessage`

	The message to be stored.

2. *string* `$strType`

	The message type. Available options:
	- **TL_ERROR** – 
		An error message.
	- **TL_CONFIRM** – 
		A confirmation message.
	- **TL_NEW** – 
		A new message.
	- **TL_INFO** – 
		An information message.
	- **TL_RAW** – 
		A raw message.
