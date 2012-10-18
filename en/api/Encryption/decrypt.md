
Encryption :: decrypt
-------------------------------------------

Decrypt a value.


### Description ###

**Definition:** `public function decrypt($varValue, $strKey=null)`

**Located in:** *system/libraries/Encryption.php*

**Class hierarchy:** *[Encryption](../Encryption.md)*


### Parameters ###

1. *mixed* `$varValue`

	Value to be decrypted.

2. *string* `$strKey`

	Key to be used in decryption process. Leave empty to use the default key (generated during installation).


### Return Values ###

Decrypted value.


### Examples ###

1. Decrypt the encrypted value

	```php
	<?php

	echo $this->Encryption->decrypt('vL4YUlTogf6b2XhrhF4sSxrklY0SsT1EJRKbN79qJWpI/h12IrBU0t47+yLEUSeVNcaeQKbBNkL0');