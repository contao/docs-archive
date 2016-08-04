# executePreActions

The `executePreActions` hook is triggered on Ajax requests that do not require a
DCA object. It passes the name of the action as argument and does not expect a
return value.

> #### tag:: Version Information 
> Available from Contao version 2.6.1.


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


## More information


### References

- [system/modules/core/classes/Ajax.php](https://github.com/contao/core/blob/3.5.0/system/modules/core/classes/Ajax.php#L173-L180)


### See also

- [executePostActions](executePostActions.md) - triggered on Ajax request that require a DCA object.
