> TODO: rewrite

# Modifying dca entries
* extension vs overwriting resources
* todo



## Altering the palette
 
... abc ... 

```php
// Example A

$GLOBALS['TL_DCA']['tl_page']['palettes']['regular'] = preg_replace(
    '~(\{meta_legend\}[^;]*;)~',
    '$1{mvo_facebook_og_legend},mvo_facebook_og_images;',
    $GLOBALS['TL_DCA']['tl_page']['palettes']['regular']
);
```


**A more structured way** to manipulate the palette string is by using the ``PaletteManipulator``. This allows for a
descriptive way to add legends and fields. 


```php
// Example B

\Contao\CoreBundle\DataContainer\PaletteManipulator::create()
    ->addLegend('assets_legend', 'webfonts_legend', \Contao\CoreBundle\DataContainer\PaletteManipulator::POSITION_BEFORE)
    ->addField('assets_collection', 'assets_legend', \Contao\CoreBundle\DataContainer\PaletteManipulator::POSITION_APPEND)
    ->applyToPalette('default', 'tl_page');
```

>Note that you can currently only add new items not remove existing ones.

>Have a look into the [PaletteManipulator.php][1] to find out more options or look how the technique is used in contao's
default bundles: for example [adding items to the ``default`` palette of``tl_layout`` in the NewsBundle][2].




[1]: https://github.com/contao/core-bundle/blob/master/src/DataContainer/PaletteManipulator.php
[2]: https://github.com/contao/news-bundle/blob/master/src/Resources/contao/dca/tl_layout.php