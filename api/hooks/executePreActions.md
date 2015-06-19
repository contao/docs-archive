# executePreActions


The `executePreActions` hook is triggered on Ajax requests that do not require a DCA object. It passes the name of the action as argument and does not expect a return value. It is available from version 2.6.1.


## Example 

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['executePreActions'][] = array('MyClass', 'myExecutePreActions');

// MyClass.php
public function myExecutePreActions($strAction)
{
    if ($strAction == 'update')
    {
        // Do something
    }
}
```


## More Information


### References

- [system/modules/backend/Ajax.php](https://github.com/contao/core/blob/2.11.7/system/modules/backend/Ajax.php#L196)


### See Also

- [executePostActions](executePostActions.md) - triggered on Ajax request that require a DCA object
