# getSystemMessages

The `getSystemMessages` hook allows to add additional messages to the back end
home screen. It does not pass any parameters and expects a string as return value.


## Return Values

Return a string with the message(s) you want to add to the home screen (including
HTML markup) or an empty string.


## Example

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['getSystemMessages'][] = array('MyClass', 'myGetSystemMessages');

// MyClass.php
public function myGetSystemMessages()
{
    $this->import('BackendUser', 'User');

    // Display a warning if the system admin's email is not set
    if ($GLOBALS['TL_ADMIN_EMAIL'] == '')
    {
        return '<p class="tl_error">Please add your email address to system settings.';
    }

    return '';
}
```


## More information


### References

- [contao/main.php](https://github.com/contao/core/blob/2.11.7/contao/main.php#L137)


### See also

- [getUserNavigation](getUserNavigation.md) – allows to manipulate the back end user navigation
