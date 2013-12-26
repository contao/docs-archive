
class System
----------------

Provide methods to manage system.


### Description ###

**Definition:** `abstract class System extends System`

**Located in:** *system/libraries/System*

**Class hierarchy:** *System*


### Methods ###

- *protected* [`import`](System/import.md) – Import a library and make it accessible by its name or an optional key
- *protected* [`log`](System/log.md) – Add a log entry
- *protected* [`addToUrl`](System/addToUrl.md) – Add a request string to the current URI string
- *protected* [`reload`](System/reload.md) – Reload the current page
- *protected* [`redirect`](System/redirect.md) – Redirect to another page
- *protected* [`getReferer`](System/getReferer.md) – Return the current referer URL and optionally encode ampersands
- *protected* [`getIndexFreeRequest`](System/getIndexFreeRequest.md) – Return the request string or an empty string if the request string is "index.php" and optionally encode ampersands
- *protected* [`loadLanguageFile`](System/loadLanguageFile.md) – Load a set of language files
- *protected* [`parseDate`](System/parseDate.md) – Parse a date format string and translate textual representations
- *protected* [`addErrorMessage`](System/addErrorMessage.md) – Add an error message
- *protected* [`addConfirmationMessage`](System/addConfirmationMessage.md) – Add a confirmation message
- *protected* [`addNewMessage`](System/addNewMessage.md) – Add a new message
- *protected* [`addInfoMessage`](System/addInfoMessage.md) – Add an info message
- *protected* [`addRawMessage`](System/addRawMessage.md) – Add a raw message
- *protected* [`addMessage`](System/addMessage.md) – Add a message
- *protected* [`getMessages`](System/getMessages.md) – Return all messages as HTML
- *protected* [`resetMessages`](System/resetMessages.md) – Reset the message system
- *protected* [`getMessageTypes`](System/getMessageTypes) – Return all available message types
- *protected* [`urlEncode`](System/urlEncode.md) – Urlencode an image path preserving slashes
- *protected* [`setCookie`](System/setCookie.md) – Set a cookie
- *protected* [`splitFriendlyName`](System/splitFriendlyName.md) – Split a friendly name address and return name and e-mail as array
- *protected* [`idnaEncode`](System/idnaEncode.md) – Encode an internationalized domain name
- *protected* [`idnaDecode`](System/idnaDecode.md) – Decode an internationalized domain name
- *protected* [`idnaEncodeEmail`](System/idnaEncodeEmail.md) – Encode an e-mail address
- *protected* [`idnaEncodeUrl`](System/idnaEncodeUrl.md) – Encode an URL
- *protected* [`isValidEmailAddress`](System/isValidEmailAddress.md) – Validate an e-mail address
- *protected* [`getReadableSize`](System/getReadableSize.md) – Convert a filesize into a human readable format
- *protected* [`getFormattedNumber`](System/getFormattedNumber.md) – Format a number
- *protected* [`anonymizeIp`](System/anonymizeIp.md) – Anonymize an IP address by overriding the last chunk

