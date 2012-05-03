printArticleAsPdf
-----------------

The `printArticleAsPdf` hook is triggered when an article is exported as PDF. It passes the article text and the article object as arguments and does not expect a return value. It is available from version 2.8.RC1.


### Example ###

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['printArticleAsPdf'][] = array('MyClass', 'myPrintArticleAsPdf');

// MyClass.php
public function myPrintArticleAsPdf($strArticle, Database_Result $objArticle)
{
    // Do something
    exit;
}
```

