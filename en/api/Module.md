
class Module
------------

Parent class for front end modules.


### Description ###

**Definition:** `abstract class Module extends System`

**Located in:** *system/modules/frontend/Module.php*

**Class hierarchy:** *[System](System.php) > [Controller](Controller.php) > [Frontend](Frontend.php) > Module*


### Methods ###

- *public* `__construct` — Initialize the object
- *public* `__set` – Set an object property
- *public* `__get` – Return an object property
- *public* [`generate`](Module/generate.md) – Parse the template
- *abstract protected* `compile` – Compile the current element
- *protected* `renderNavigation` – Recursively compile the navigation menu and return it as HTML string


### Properties ###

- *protected* `$strTemplate`
- *protected* `$strColumn`
- *protected* `$arrData`
- *protected* `$arrStyle`
