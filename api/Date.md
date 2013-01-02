class Date
----------

Provide methods to handle different date formats.

### Description ###

**Located in:** *system/libraries/Date.php*

**Class hierarchy:** *[System](System.md) > Date*



### Methods ###

- *public* [`__construct`](Date/__construct.md) – Create object properties and date ranges
- *public* [`__get`](Date/__get.md) – Return an object property
- *public* [`getWeekBegin`](Date/getWeekBegin.md) – Return the begin of the week as timestamp
- *public* [`getWeekEnd`](Date/getWeekEnd.md) – Return the end of the week as timestamp
- *public* [`getRegexp`](Date/getRegexp.md) – Return a regular expression to check a date
- *protected* [`getRegexpCallback`](Date/getRegexpCallback.md) – Callback function for getRegexp
- *public* [`getInputFormat`](Date/getInputFormat.md) – Return an input format string for a particular date (e.g. YYYY-MM-DD)
- *protected* [`dateToUnix`](Date/dateToUnix.md) – Convert a date string into a UNIX timestamp using a particular date format
- *public* [`formatToJs`](Date/formatToJs.md) – Convert a PHP format string into a JavaScript format string


### Properties ###
 
- *protected* `$intTstamp` - Timestamp
- *protected* `$strFormat` - Format string
- *protected* `$strDate` - Date
- *protected* `$strTime` - Time
- *protected* `$strDatim` - Date and time
- *protected* `$arrRange` - Date range array
