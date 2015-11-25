# Finding the right template variables
When writing templates, you often need to use template variables - for example for getting image sizes. There are several methods to obtain them

### $this->showTemplateVars()
In every Contao Frontend Template you can use ```$this->showTemplateVars();```, this methods prints most of the available template variables. This method is defined in [/system/modules/core/library/Contao/Template.php][0].
As you can see in the source, the output is wrapped in ```<pre>``` tags.

### print_r($this)
To also find out about available methods or get more information, you can use ```print_r($this);```, this will print all information about available methods, instances of classes or variables.
To get more information about used classes, that are in the output of the ```print_r``` statement, you can just [look up their source code in the repo][1].

### Using methods in productive envoirements
If you are editing your template in a productive envoirement, it is recommended to wrap the output with HTML comment tags.
```php
<!-- <?php print_r($this); ?> -->
```

[0]: https://github.com/contao/core/blob/master/system/modules/core/library/Contao/Template.php#L238
[1]: https://github.com/contao/core/find/master
