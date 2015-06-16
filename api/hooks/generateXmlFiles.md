# generateXmlFiles

The `generateXmlFiles` hook is triggered when the XML files are (re)generated
e.g. by clicking "System -> Maintenance -> Recreate the XML files" in the back end.
It has no parameters and does not expect a return value.
It is available from version 3.0.0-beta1.


## Parameters

The hook has no parameters

## Example

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


## More Information


### References

- [system/modules/core/library/Contao/Automator.php](https://github.com/contao/core/blob/support/3.2/system/modules//core/library/Contao/Automator.php#L249)
