executePostActions
------------------

The `executePostActions` hook is triggered on Ajax requests that require a DCA object. It passes the name of the action and the data container object as arguments and does not expect a return value. It is available from version 2.6.1.


### Example ###

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['executePostActions'][] = array('MyClass', 'myExecutePostActions');

// MyClass.php
public function myExecutePostActions($strAction, DataContainer $dc)
{
    if ($strAction == 'update')
    {
        // Do something
    }
}
```


### References ###

- [system/modules/backend/Ajax.php](https://github.com/contao/core/blob/2.11.7/system/modules/backend/Ajax.php#L345)


### See Also ###

- [executePreActions](executePreActions.md) - triggered on Ajax request that do not require a DCA object