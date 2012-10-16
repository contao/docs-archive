
Environment :: __get
-------------------------------------------

Return an environment parameter.


### Description ###

**Definition:** `public function __get($strKey)`

**Located in:** *system/libraries/Environment*

**Class hierarchy:** *[Environment](../Environment.md)*


### Parameters ###

1. *string* `$strKey`

	Name of the parameter to be returned. Return null, if parameter is not found. Available parameters:
	- **scriptFilename** -
		The absolute path to the script (e.g. /home/www/html/website/index.php).
	- **scriptName** -
		The relative path to the script (e.g. /website/index.php).
	- **phpSelf** -
		The relative path to the script (e.g. /website/index.php).
	- **documentRoot** -
		The document root (e.g. /home/www/user/). Calculated as SCRIPT_FILENAME minus SCRIPT_NAME as some CGI versions mod-rewrite rules might return an incorrect DOCUMENT_ROOT.
	- **requestUri** -
		The request URI [path]?[query] (e.g. /contao/index.php?id=2).
	- **httpAcceptLanguage** -
		The first eight user languages as array.
	- **httpAcceptEncoding** -
		Accepted encoding types as array.
	- **httpUserAgent** -
		The user agent as string.
	- **httpHost** -
		The HTTP Host.
	- **httpXForwardedHost** -
		The HTTP X-Forwarded-Host.
	- **ssl** -
		True if the current page was requested via an SSL connection.
	- **url** -
		The current URL without path or query string.
	- **ip** -
		The real REMOTE_ADDR even if a proxy server is used.
	- **server** -
		The SERVER_ADDR.
	- **path** -
		The relative path to the base directory (e.g. /path).
	- **script** -
		The relative path to the script (e.g. index.php).
	- **request** -
		The relative path to the script and include the request (e.g. index.php?id=2).
	- **base** -
		The current URL and path that can be used in a <base> tag.
	- **host** -
		The current host name.
	- **isAjaxRequest** -
		True on Ajax requests.
	- **agent** -
		The operating system and the browser name and version.


### Return Values ###

Mixed values.

