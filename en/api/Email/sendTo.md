
Email :: sendTo
-------------------------------------------

Get e-mail addresses from an array, string or unlimited number of arguments and send the e-mail. Friendly name portions (e.g. Admin <admin@example.com>) are allowed.


### Description ###

**Definition:** `public function sendTo()`

**Located in:** *system/libraries/Email*

**Class hierarchy:** *[System](../System.php) > [Email](../Email)*


### Parameters ###

1. *mixed*

	Recipients that will receive an e-mail.
	- **an e-mail address** -
		admin@example.com
	- **a friendly e-mail address** – 
		Admin <admin@example.com>
	- **a set of e-mail addresses** – 
		admin@example.com, User <user@example.com>
	- **an array e-mail addresses** – 
		Array ( [0] => admin@example.com, [1] => User <user@example.com> )


### Return Values ###

True if the e-mail was sent successfully, false otherwise.