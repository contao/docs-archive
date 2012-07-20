
Email :: sendBcc
-------------------------------------------

Get BCC e-mail addresses from an array, string or unlimited number of arguments. Friendly name portions (e.g. Admin <admin@example.com>) are allowed.


### Description ###

**Definition:** `public function sendBcc()`

**Located in:** *system/libraries/Email*

**Class hierarchy:** *[System](../System.php) > [Email](../Email)*


### Parameters ###

1. *mixed*

	Recipients that will receive a blind carbon copy.
	- **an e-mail address** -
		admin@example.com
	- **a friendly e-mail address** – 
		Admin <admin@example.com>
	- **a set of e-mail addresses** – 
		admin@example.com, User <user@example.com>
	- **an array e-mail addresses** – 
		Array ( [0] => admin@example.com, [1] => User <user@example.com> )
	

### See Also ###

- [`Email::sendCc`](sendCc.md) – Send the recipients of carbon copy
