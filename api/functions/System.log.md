
# System :: log()

Add a log entry.


## Description

```php
public static function log($strText, $strFunction, $strAction)
```

**Location in Contao 3:** [*system/modules/core/library/Contao/System.php*][contao3]<br>
**Location in Contao 4:** [*vendor/contao/core-bundle/src/Resources/contao/library/Contao/System.php*][contao4]


## Parameters

1. *string* `$strText`

    The text to be logged.

2. *string* `$strFunction`

    The name of the function where log is made.
    
    > **Hint** Consider using the PHP constant `__METHOD__` 
    > instead of manually writing the function name.

3. *string* `$strCategory`

    A type of the log message. Available constants:
    
    - **TL_ERROR** – An error message.
    - **TL_ACCESS** – A message that relates to the access.
    - **TL_GENERAL** – A general message.
    - **TL_FILES** – A message that relates to the files.
    - **TL_CRON** – A message that relates to the cron jobs.
    - **TL_FORMS** – A message that relates to the forms.
    - **TL_CONFIGURATION** – A message that relates to the configuration.
    - **TL_NEWSLETTER** – A message that relates to the newsletter.
    - **TL_REPOSITORY** – A message that relates to the extension repository.
    

## Examples

1. Log that an e-mail was sent

    ```php
    <?php

    // ModuleCustom::sendEmail()
    \System::log('The e-mail was sent successfully', __METHOD__, TL_GENERAL);
    ```


[contao3]: https://github.com/contao/core/blob/3.5.0/system/modules/core/library/Contao/System.php#L167-L199
[contao4]: https://github.com/contao/core-bundle/blob/4.0.0/src/Resources/contao/library/Contao/System.php#L202-L234
