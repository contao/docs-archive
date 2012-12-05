setCookie
---------

The `setCookie` hook is triggered when sending a cookie to the browser. It passes a standard object with all cookie properties and expects the same as return value. Added in Contao 2.11.3.


### Parameters ###

1. *object* `$objCookie`

	A stdClass instance that contains the properties of the cookie. See PHP's [setcookie](http://php.net/setcookie) documentation for detailed information.
	- $objCookie->strName		*– the cookie name*
	- $objCookie->varValue		*– the cookie value*
	- $objCookie->intExpires	*– the expiration time (in seconds, from now)*
	- $objCookie->strPath		*– the relative path (if Contao is installed in a subfolder)*
	- $objCookie->strDomain		*– the current domain for the cookie*
	- $objCookie->blnSecure		*– if the cookie should only be stored for https access*


### Return Values ###

Return `$objCookie` or a custom object with all properties.


### Example ###

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['setCookie'][] = array('MyClass', 'mySetCookie');

// MyClass.php
public function mySetCookie($objCookie)
{
	// Make sure the cookie is also valid for the whole domain
	$objCookie->strPath = '/';

	return $objCookie;
}
```


### References ###

- [system/libraries/System.php](https://github.com/contao/core/blob/2.11.7/system/libraries/System.php#L720)
