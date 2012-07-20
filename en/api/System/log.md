
System :: log
-------------------------------------------

Add a log entry.


### Description ###

**Definition:** `protected function log($strText, $strFunction, $strAction)`

**Located in:** *system/libraries/System*

**Class hierarchy:** *[System](../System.md)*


### Parameters ###

1. *string* `$strText`

	The text to be logged.

2. *string* `$strFunction`

	The name of the function where log is made.

3. *string* `$strAction`

	A type of the log message. Available options:
	- **TL_ERROR** – 
		An error message.
	- **TL_ACCESS** – 
		A message that relates to the access.
	- **TL_GENERAL** – 
		A general message.
	- **TL_FILES** – 
		A message that relates to the files.
	- **TL_CRON** – 
		A message that relates to the cron jobs.
	- **TL_FORMS** – 
		A message that relates to the forms.
	- **TL_CONFIGURATION** – 
		A message that relates to the configuration.
	- **TL_NEWSLETTER** – 
		A message that relates to the newsletter.
	- **TL_REPOSITORY** – 
		A message that relates to the extension repository.
	

### Examples ###

1. Log that e-mail was sent

	```php
	<?php

	// ModuleCustom::sendEmail()
	$this->log('The e-mail was sent successfully', 'ModuleCustom sendEmail()', TL_GENERAL);
	```

