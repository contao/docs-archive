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


### See Also ###

- [executePreActions](executePreActions.md) - triggered on Ajax request that do not require a DCA object