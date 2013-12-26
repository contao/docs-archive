
System :: anonymizeIp
-------------------------------------------

Anonymize an IP address by overriding the last chunk.


### Description ###

**Definition:** `protected function anonymizeIp($strIp)`

**Located in:** *system/libraries/System*

**Class hierarchy:** *[System](../System.md)*


### Parameters ###

1. *string* `$varNumber`

	The IP address that should be anonymized. Note that the IP addresses 127.0.0.1 and ::1 will be returned in the unchanged form.


### Return Values ###

The anonymized IP address.
	

### Examples ###

1. Anonymize a custom IP address

	```php
	<?php

	echo $this->anonymizeIp('136.34.142.2');
	```
	> 136.34.142.0

