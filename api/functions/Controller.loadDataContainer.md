
# Controller :: loadDataContainer()

Load a set of DCA files.


## Description

```php
public static function loadDataContainer($strName, $blnNoCache = false)
```

**Location in Contao 3:** [*system/modules/core/library/Contao/Controller.php*][contao3]<br>
**Location in Contao 4:** [*vendor/contao/core-bundle/src/Resources/contao/library/Contao/Controller.php*][contao4]


## Parameters

1. *string* `$strName`

    Name of the data container to be loaded.

1. *boolean* `$blnNoCache`

    If set to true, the cache will not be used.


## Examples

1. Display the tl_news parent table

    ```php
    <?php

    \Controller::loadDataContainer('tl_news');
    echo $GLOBALS['TL_DCA']['tl_news']['config']['ptable'];
    ```
    > tl_news_archive


[contao3]: https://github.com/contao/core/blob/3.5.0/system/modules/core/library/Contao/Controller.php#L1249-L1259
[contao4]: https://github.com/contao/core-bundle/blob/4.0.0/src/Resources/contao/library/Contao/Controller.php#L1229-L1239
