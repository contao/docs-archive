## Customizing TinyMCE

This page explains how to customize the Rich Text Editor and save the changes so
they will not be overridden on the next Contao update. Note that Contao does not
include all TinyMCE plugins by default, so if you want to use a certain plugin
that is not part of the Contao distribution, download it from the [TinyMCE
project website][1] and move it into the `assets/tinymce/plugins` folder.

![](images/rich-text-editor.jpg?raw=true)

The image above shows the default Rich Text Editor configuration file
`system/config/tinyMCE.php`. To create a custom configuration file, simply copy
it and rename it e.g. to `tinyCustom.php`. Then apply your changes and save the
new file. The last step is to adjust the [data container configuration][2] in
the `system/config/dcaconfig.php` file and tell Contao to which fields the
custom file shall be applied.

```php
// Use the custom RTE configuration for text elements
$GLOBALS['TL_DCA']['tl_content']['fields']['text']['eval']['rte'] =
'tinyCustom';
```


[1]: http://tinymce.moxiecode.com
[2]: ../07-customizing-contao/custom-configurations.md#customizing-the-data-container-configuration