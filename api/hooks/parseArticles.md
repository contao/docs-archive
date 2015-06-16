# parseArticles


The `parseArticles` hook is triggered when parsing news articles. It passes the frontend template, the current article and the news module instance. It does not expect a return value.


## Parameters 

1. *FrontendTemplate* `$objTemplate`

	The frontend template instance for the news article (e.g. `news_full`).

2. *array* `$arrRow`

	The current news item database result.

3. *ModuleNews* `$objModule`

	The news module instance (e.g. `ModuleNewsList`).


## Example 

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['parseArticles'][] = array('MyClass', 'myParseArticles');

// MyClass.php
public function myParseArticles($objTemplate, $arrRow, $objModule)
{
	// Remove the default "by XXX" from Contao
    $objTemplate->author = $arrRow['author'];
}
```


## More Information


### References

- [system/modules/news/ModuleNews.php](https://github.com/contao/core/blob/2.11.7/system/modules/news/ModuleNews.php#L206)


### See Also

- [getAllEvents](getAllEvents.md) – allows you to modify the result sets of calendar and event modules
