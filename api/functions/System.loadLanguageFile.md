
# System :: loadLanguageFile()

Load a set of language files.


## Description

```php
public static function loadLanguageFile($strName, $strLanguage = false, $blnNoCache = false)
```

**Location in Contao 3:** [*system/modules/core/library/Contao/System.php*][contao3]<br>
**Location in Contao 4:** [*vendor/contao/core-bundle/src/Resources/contao/library/Contao/System.php*][contao4]


## Parameters

1. *string* `$strName`

    Name of the language files (e.g. *countries* to access `$GLOBALS['TL_LANG']['CNT']`).

2. *string* `$strLanguage`

    An optional language key. If none provided, the current one will be used.

3. *boolean* `$blnNoCache`

    If set to true, the cache will not be used.


## Examples

1. Load the countries language files

    ```php
    <?php

    \System::loadLanguageFile('countries');
    echo $GLOBALS['TL_LANG']['CNT']['pl'];
    ```
    > Poland


[contao3]: https://github.com/contao/core/blob/3.5.0/system/modules/core/library/Contao/System.php#L255-L355
[contao4]: https://github.com/contao/core-bundle/blob/4.0.0/src/Resources/contao/library/Contao/System.php#L293-L412
