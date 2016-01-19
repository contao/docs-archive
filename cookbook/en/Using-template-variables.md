# Using template variables

When writing templates, you often need to use template variables,
for example for getting image sizes. There are several ways to obtain them.


## Methods

### `$this->showTemplateVars()`

In every Contao Template you can use `$this->showTemplateVars();`,
which prints the available template variables. This method is defined
in [/system/modules/core/library/Contao/Template.php][0]. As you can see in 
the source, the output is wrapped in `<pre>` tags for improved readability.


### `print_r($this)`

If you want to get more information you can use `print_r($this);`. 
That will print all information about available methods, instances of classes
or variables. To get more information about used classes that are in the output 
of the `print_r` statement, you can just 
[look up their source code in the repository][1].


## Live websites

If you are editing your template in a live website, wrapping the
output with HTML comment tags is recommended.

```php
<!-- <?php print_r($this); ?> -->
```


## Serialized arrays

Template variables may be [serialized][2] arrays. You have to unserialize
them before using.

```php
$arr = array("key" => "value");
$seArray = serialize($arr);
echo $seArray;
//Prints: a:1:{s:3:"key";s:5:"value";}
$realArray = deserialize($seArray);
```



[0]: https://github.com/contao/core/blob/master/system/modules/core/library/Contao/Template.php#L238
[1]: https://github.com/contao/core/find/master
[2]: http://php.net/manual/en/language.oop5.serialization.php
