# compileArticle

The `compileArticle` hook is triggered after the article module has been compiled. It passes the template object, the module configuration, and the module object as arguments and expects no return value. 
> **tag** It is available from version 3.5.0.


## Parameters ##

1. *FrontendTemplate* `$objTemplate`

    The current frontend template instance for the article module

2. *array* `$arrData`

    An associative array with the module configuration

3. *ModuleArticle* `$objModule`

    The current module instance


## Example ##

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['compileArticle'][] = array('MyClass', 'myCompileArticle');

// MyClass.php
public function myCompileArticle($objTemplate, $arrData, $objModule)
{

}
```


## More Information ##


### References ###

- [system/modules/ModuleArticle.php](https://github.com/contao/core/blob/master/system/modules/core/modules/ModuleArticle.php#L267)