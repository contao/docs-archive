
Encryption :: encrypt
-------------------------------------------

Encrypt a value.


### Description ###

**Definition:** `public function encrypt($varValue, $strKey=null)`

**Located in:** *system/libraries/Encryption.php*

**Class hierarchy:** *[Encryption](../Encryption.md)*


### Parameters ###

1. *mixed* `$varValue`

	Value to be encrypted.

2. *string* `$strKey`

	Key to be used in encryption process. Leave empty to use the default key (generated during installation).


### Return Values ###

Encrypted value.


### Examples ###

1. Encrypt the user e-mail address

	```php
	<?php

	echo $this->Encryption->encrypt($this->User->email);