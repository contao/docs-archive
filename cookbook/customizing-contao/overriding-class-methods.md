## Overriding class methods

Let us assume that you want to modify the behaviour of the navigation module to
always display even if there are no sub-pages and the module would not be shown
at all. In this case a note shall be printed to inform the user that there are
no sub-pages. Of course we will try to preserve as much of the original
navigation class as possible, so future updates do not require maintenance.
Module and content element classes can be assigned dynamically in the Contao
system configuration, which allows you to easily replace them with your own
versions.


### Creating a custom class

The default navigation class behaves pretty much like we want it to, except that
the `generate()` method hides the module if there are no sub-pages. Therefore
all we need to change is this particular method, so the best practice is to
extend the original class and simply override it. To do so, create a new
`xcustom/ModuleMyNavigation.php` file and define the custom class
`ModuleMyNavigation`:

```php
// xcustom/ModuleMyNavigation.php
class ModuleMyNavigation extends ModuleNavigation
{
    public function generate()
    {
        // Execute the original method
        $buffer = parent::generate();

        if (empty($buffer))
        {
            $buffer = 'There are no subpages';
        }

        return $buffer;
    }
}
```


### Registering a custom class

Module and content element classes can be assigned dynamically in the Contao
system configuration, which allows you to easily replace them with your own
versions. The names of the module classes are stored in the global `FE_MOD`
array.

```php
// xcustom/config/config.php
$GLOBALS['FE_MOD']['navigationMenu']['navigation'] = 'ModuleMyNavigation';
```

Thanks to the dynamic configuration, Contao automatically loads the new class
upon the next request and the navigation module prints the "There are no
subpages" notice instead of not displaying at all. The modification is
update-safe and does not require maintenance.
