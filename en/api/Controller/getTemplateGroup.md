
Controller :: getTemplateGroup
-------------------------------------------

Return all template files of a particular group as array.


### Description ###

**Definition:** `protected function getTemplateGroup($strPrefix, $intTheme=0)`

**Located in:** *system/libraries/Controller.php*

**Class hierarchy:** *[System](../System.php) > [Controller](../Controller.php)*

**Throws:** *Exception*


### Parameters ###

1. *string* `$strPrefix`

	A template group prefix.

2. *integer* `$intTheme`

	The theme ID to search in.


### Return Values ###

An array of available templates with specified prefix.


### Examples ###

1. Get all templates with *news_* prefix as array

	```php
	<?php

	print_r($this->getTemplateGroup('news_');
	```
	> Array ( [0] => news_full [1] => news_latest [2] => news_short [3] => news_simple )


2. Get all templates with *news_* prefix of the current theme as array (commonly used in tl_module)

	```php
	<?php

	public function getNewsTemplates(DataContainer $dc)
	{
		$intPid = $dc->activeRecord->pid;

		if ($this->Input->get('act') == 'overrideAll')
		{
			$intPid = $this->Input->get('id');
		}

		return $this->getTemplateGroup('news_', $intPid);
	}
	```
