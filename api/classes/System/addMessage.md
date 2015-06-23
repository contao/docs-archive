
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


### See also ###

- [`System::addConfirmationMessage`](addConfirmationMessage.md) – Add a confirmation message
- [`System::addErrorMessage`](addErrorMessage.md) – Add an error message
- [`System::addInfoMessage`](addInfoMessage.md) – Add an info message
- [`System::addNewMessage`](addNewMessage.md) – Add a new message
- [`System::addRawMessage`](addRawMessage.md) – Add a raw message
- [`System::getMessages`](getMessages.md) – Get messages as HTML
- [`System::getMessageTypes`](getMessageTypes.md) – Get message types
- [`System::resetMessages`](resetMessages.md) – Reset system messages
