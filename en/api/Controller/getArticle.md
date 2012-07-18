
Controller :: getArticle
-------------------------------------------

Generate an article with specified ID or alias and return it as string.


### Description ###

**Definition:** `protected function getArticle($varId, $blnMultiMode=false, $blnIsInsertTag=false, $strColumn='main')`

**Located in:** *system/libraries/Controller.php*

**Class hierarchy:** *[System](../System.php) > [Controller](../Controller.php)*


### Parameters ###

1. *mixed* `$varId`

	The numberic ID or alias of the article.

2. *boolean* `$blnMultiMode`

	If set to true, only article teaser will be displayed (useful when displaying a list of articles).

3. *boolean* `$blnIsInsertTag`

	If set to true, the plain article will be returned - without surrounding *div* container, only parsed content elements.

4. *string* `$strColumn`

	The column which article is generated in.


### Examples ###

1. Display the article with the ID of 123

	```php
	<?php

	echo $this->getArticle(123);
	```

2. Display the article teaser with the alias *welcome-to-music-academy*

	```php
	<?php

	echo $this->getArticle('welcome-to-music-academy', true);
	```
