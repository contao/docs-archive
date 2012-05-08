
class Email
-----------

Provide methodes to send e-mails.


### Description ###

**Definition:** `class Email extends System`

**Located in:** *system/libraries/Email.php*

**Class hierarchy:** *[System](System.php) > Email*


### Methods ###

- *public* `__construct()` – Instantiate object and load Swift plugin
- *public* `__set` – Set an object property
- *public* `__get` – Return an object property
- *public* `hasFailures` – Return true if there are failures
- *public* `addHeader` – Add a custom text header
- *public* `sendCc` – Get CC e-mail addresses from an array, string or unlimited number of arguments
- *public* `sendBcc` – Get BCC e-mail addresses from an array, string or unlimited number of arguments
- *public* `replyTo` – Get ReplyTo e-mail addresses from an array, string or unlimited number of arguments
- *public* `attachFile` – Attach a file
- *public* `attachFileFromString` – Attach a file from a string
- *public* `sendTo` – Get e-mail addresses from an array, string or unlimited number of arguments and send the e-mail
- *protected* `compileRecipients` – Compile e-mail addresses from an array of (different) arguments
