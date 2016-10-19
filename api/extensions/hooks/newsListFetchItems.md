# newsListFetchItems

The `newsListFetchItems` hook is triggered when news list items are fetched
from database.

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

3. *int* `$limit`

    Number of items that should be displayed.

4. *int* `$offset`

    Offset of items to skip.

5. *ModuleNewsList* `$newsListModule`

    The news list module that was used to fetch items.


## Example

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['newsListFetchItems'][] = array('MyClass', 'myNewsListFetchItems');

// MyClass.php
public function myNewsListFetchItems($newsArchives, $blnFeatured, $limit, $offset, \ModuleNewsList $newsListModule)
{
    // Do something
}
```


## More information


### References

- [system/modules/core/modules/ModuleNewsList.php](https://github.com/contao/core/blob/3.5.17/system/modules/news/modules/ModuleNewsList.php#L203)


### See also

- [newsListCountItems](newsListCountItems.md) - triggered when the number of
news items is needed (before fetching a news list).
