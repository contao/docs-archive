# newsListCountItems

The `newsListCountItems` hook is triggered when the number of news items is
needed (before fetching a news list).

> #### primary:: Available   
> from Contao 3.5.0.


## Parameters

1. *array* `$newsArchives`

    An array containing news archives IDs.

2. *boolean* `$blnFeatured`

    A boolean that indicates if the news list must display featured news.
    Possible values are:
    - `null` (display all news)
    - `true` (display only featured news)
    - `false` (display all news that are not featured)


## Example

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['newsListCountItems'][] = array('MyClass', 'myNewsListCountItems');

// MyClass.php
public function myNewsListCountItems($newsArchives, $blnFeatured)
{
    // Do something
}
```


## More information


### References

- [system/modules/core/modules/ModuleNewsList.php](https://github.com/contao/core/blob/3.5.17/system/modules/news/modules/ModuleNewsList.php#L170)


### See also

- [newsListFetchItems](newsListFetchItems.md) - triggered when news list items
are fetched from database.
