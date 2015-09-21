
# Controller :: redirect()

Redirect to another page.


## Description

```php
public static function redirect($strLocation, $intStatus = 303)
```

**Location in Contao 3:** [*system/modules/core/library/Contao/Controller.php*][contao3]<br>
**Location in Contao 4:** [*vendor/contao/core-bundle/src/Resources/contao/library/Contao/Controller.php*][contao4]


## Parameters

1. *string* `$strLocation`

    The destination URL (relative to Contao base or an absolute URL).

2. *integer* `$intStatus`

    A valid [HTTP status code][code].
    - **301** – Moved Permanently
    - **302** – Found
    - **303** – See Other *(default)*


## Examples

1. Redirect to the calendar page

    ```php
    <?php

    \Controller::redirect('calendar.html');
    ```


[contao3]: https://github.com/contao/core/blob/3.5.0/system/modules/core/library/Contao/Controller.php#L1013-L1066
[contao4]: https://github.com/contao/core-bundle/blob/4.0.0/src/Resources/contao/library/Contao/Controller.php#L996-L1025
[code]:    https://en.wikipedia.org/wiki/List_of_HTTP_status_codes#3xx_Redirection
