# Using the right template variables

Here are some useful examples for using template variables.

### Template variables for displaying embedded images

|Variable   	|Data Type  |Possible Content   	|Explanation  |
|---	|---	|---	|---	|---	|
|addImage   	|**Boolean**   	|*True / False*   	|If its true, there is an image that should be embedded   	|
|singleSRC   	|String   	|path/to/img.jpg   	|Path to the image   	|
|alt   	|String   	|Alternative Text   	|Alternative text
|size   	|Array*   	|a:3:{i...   	|Serialized Array with size & dimension information  |
|imagemargin   	|Array*   	|a:5:{   	|Serialized Array with margin information   	|
|fullsize   	|Boolean   	|True / False   	|Image should open in a new window or lightbox   	|
|caption   	|String   	|   	|Caption for the image / lightbox entry   	|
|floating   	|String   	|left / right / above / below   	|Floating behaviour of the image   	|

* It's a serialized array, so you have to deserialize it:
```php
	$imageSize = deserialize($this->size);
	$imageMargin = deserialize($this->imagemargin);
```
