
Email :: __construct
-------------------------------------------

Create a new Email object.


### Description ###

**Definition:** `public function __construct()`

**Located in:** *system/libraries/Email.php*

**Class hierarchy:** *[System](../System.md) > [Email](../Email.md)*


### Examples ###

1. Send a welcome e-mail

	```php
	<?php

	$objEmail = new Email();
	$objEmail->from = $GLOBALS['TL_ADMIN_EMAIL'];
	$objEmail->subject = 'Welcome to Music Academy';
	$objEmail->text = 'We are glad to have you on board!';
	$objEmail->sendCc($GLOBALS['TL_ADMIN_EMAIL']);
	$objEmail->sendTo('d.evans@example.com');
	```

