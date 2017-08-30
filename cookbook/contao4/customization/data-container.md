# Modifying dca entries

## Altering palettes
 
Does this look familiar to you? Using regular expressions or ``str_replace`` to
alter a palette of an existing data container?

```php
// the hard/unclear way

$GLOBALS['TL_DCA']['tl_page']['palettes']['regular'] = preg_replace(
    '~(\{meta_legend\}[^;]*;)~',
    '$1{my_bundle_abc_legend},my_bundle_abc_field;',
    $GLOBALS['TL_DCA']['tl_page']['palettes']['regular']
);
```


**A more structured way** to manipulate the palette string is by using the
``PaletteManipulator``. This allows for a descriptive way to add legends and
fields.


```php
// the neat way

\Contao\CoreBundle\DataContainer\PaletteManipulator::create()
    ->addLegend('my_bundle_abc_legend', 'meta_legend', \Contao\CoreBundle\DataContainer\PaletteManipulator::POSITION_BEFORE)
    ->addField('my_bundle_abc_field', 'my_bundle_abc_legend', \Contao\CoreBundle\DataContainer\PaletteManipulator::POSITION_APPEND)
    ->applyToPalette('regular', 'tl_page');
```

> #### info:: Info
> Note that you can currently only add new items not remove existing ones.

Have a look into the [PaletteManipulator][1] to find out more options or see
how the technique is used in Contao's default bundles: for example 
[adding items to the ``default`` palette of``tl_layout``][2] by the
``NewsBundle``.




[1]: https://github.com/contao/core-bundle/blob/master/src/DataContainer/PaletteManipulator.php
[2]: https://github.com/contao/news-bundle/blob/master/src/Resources/contao/dca/tl_layout.php