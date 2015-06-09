------------
generateXmlFiles

The `generateXmlFiles` hook is triggered when the XML files are (re)generated
e.g. by clicking "System -> Maintenance -> Recreate the XML files" in the backend.
It has no parameters an no return value.


### Parameters ###

The hook has no parameters

### Example ###

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['generateXmlFiles'][] = array('MyClass', 'myGenerateXmlFiles');

// MyClass.php
public function myGenerateXmlFiles()
{
    // see
    // generateFeeds() in
    // system/modules/calendar/classes/Calendar.php
    // or
    // system/modules/news/classes/News.php
    // for examples.
}
```


### References ###

- [system/modules/core/library/Contao/Automator.php](https://github.com/contao/core/blob/support/3.2/system/modules//core/library/Contao/Automator.php#L249)

### See Also ###

- [system/modules/calendar/config/config.php](https://github.com/contao/core/blob/3.3.20/system/modules/calendar/config/config.php#L53)
- [system/modules/news/config/config.php](https://github.com/contao/core/blob/3.3.20/system/modules/news/config/config.php#L52)
