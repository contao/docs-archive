
class Input
-----------

Provide methods to clean up user input and to prevent XSS.


### Description ###

**Definition:** `class Input`

**Located in:** *system/libraries/Input.php*

**Class hierarchy:** *Input*


### Methods ###

- *public* [`getInstance`](Input/getInstance.md) – Return the current object instance (Singleton)
- *public* [`get`](Input/get.md) – Return a $_GET parameter
- *public* [`post`](Input/post.md) – Return a $_POST parameter
- *public* [`postHtml`](Input/postHtml.md) – Return a $_POST parameter preserving allowed HTML tags
- *public* [`postRaw`](Input/postRaw.md) – Return a $_POST parameter unencoded without stripping tags
- *public* [`cookie`](Input/cookie.md) – Return a $_COOKIE parameter
- *public* [`setGet`](Input/setGet.md) – Set a $_GET parameter
- *public* [`setPost`](Input/setPost.md) – Set a $_POST parameter
- *public* [`setCookie`](Input/setCookie.md) – Set a $_COOKIE parameter
- *public* [`resetCache`](Input/resetCache.md) – Reset the internal cache


### Properties ###

- *protected static* `$objInstance` - Current object instance (Singleton)
- *protected* `$arrCache` - Cache array
- *protected* `$blnMagicQuotes` - Magic quotes
