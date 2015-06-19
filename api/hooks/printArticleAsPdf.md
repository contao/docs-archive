# printArticleAsPdf


The `printArticleAsPdf` hook is triggered when an article should be exported as PDF. It passes the article text and the article object as arguments and does not expect a return value. Use it to override the internal PDF functionality. It is available from version 2.8.RC1.


## Parameters 

1. *string* `$strArticle`

	The compiled article content.

2. *Database_Result* `$objArticle`

	Article database result from table `tl_article`.


## Example 

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['printArticleAsPdf'][] = array('MyClass', 'myPrintArticleAsPdf');

// MyClass.php
public function myPrintArticleAsPdf($strArticle, Database_Result $objArticle)
{
    // Trigger your own PDF engine and exit
    exit;
}
```


## More Information


### References

- [system/libraries/Controller.php](https://github.com/contao/core/blob/2.11.7/system/libraries/Controller.php#L1317)
