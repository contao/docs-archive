# Finding the right template variables

When writing templates, you often need to use template variables, for example for getting image sizes. There are several methods to obtain them.

#### $this->showTemplateVars()
In every Contao Frontend Template you can use ```$this->showTemplateVars();```, it prints most of the available template variables. This method is defined in [/system/modules/core/library/Contao/Template.php][0].
As you can see in the source, the output is wrapped in ```<pre>``` tags.

#### print_r($this)
If you want to get more information you can use ```print_r($this);```. That will print all information about available methods, instances of classes or variables.
To get more information about used classes that are in the output of the ```print_r``` statement, you can just [look up their source code in the repository][1].

## Using methods in productive environments

If you are editing your template in a productive environment wrapping the output with HTML comment tags is recommended.
```php
<!-- <?php print_r($this); ?> -->
```

## Serialized arrays
Template varaibles may contain [serialized][2] arrays. You have to deserialize them before using.
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
