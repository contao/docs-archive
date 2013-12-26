
class Email
-----------

Provide methods to send e-mails.


### Description ###

**Definition:** `class Email extends System`

**Located in:** *system/libraries/Email.php*

**Class hierarchy:** *[System](System.md) > Email*


### Methods ###

- *public* [`__construct()`](Email/__construct.md) – Instantiate object and load Swift plugin
- *public* [`__set`](Email/__set.md) – Set an object property
- *public* [`__get`](Email/__get.md) – Return an object property
- *public* [`hasFailures`](Email/hasFailures.md) – Return true if there are failures
- *public* [`addHeader`](Email/addHeader.md) – Add a custom text header
- *public* [`sendCc`](Email/sendCc.md) – Get CC e-mail addresses from an array, string or unlimited number of arguments
- *public* [`sendBcc`](Email/sendBcc.md) – Get BCC e-mail addresses from an array, string or unlimited number of arguments
- *public* [`replyTo`](Email/replyTo.md) – Get ReplyTo e-mail addresses from an array, string or unlimited number of arguments
- *public* [`attachFile`](Email/attachFile.md) – Attach a file
- *public* [`attachFileFromString`](Email/attachFileFromString.md) – Attach a file from a string
- *public* [`sendTo`](Email/sendTo.md) – Get e-mail addresses from an array, string or unlimited number of arguments and send the e-mail
- *protected* [`compileRecipients`](Email/compileRecipients.md) – Compile e-mail addresses from an array of (different) arguments
