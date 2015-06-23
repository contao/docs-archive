# compileArticle

The `compileArticle` hook is triggered after the article module has been compiled. It passes the template object, the module configuration, and the module object as arguments and does not expect a return value. It can be used e.g. to add additional data to the template.
> **tag** It is available from version 3.5.0.


## Parameters

1. *FrontendTemplate* `$objTemplate`

    The current front end template instance for the article module

2. *array* `$arrData`

    An associative array with the module configuration

3. *ModuleArticle* `$objModule`

    The current module instance


## Example

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['compileArticle'][] = array('MyClass', 'myCompileArticle');

// MyClass.php
public function myCompileArticle($objTemplate, $arrData, $objModule)
{
    $objTemplate->customContent = '<p>This will be available in mod_article.html5 via $this->customContent</p>';
}
```


## More Information


### Reference

- [system/modules/ModuleArticle.php](https://github.com/contao/core/blob/master/system/modules/core/modules/ModuleArticle.php#L267)