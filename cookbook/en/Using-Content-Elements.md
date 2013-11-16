# Using content elements in your own extension

As of Contao 3.0 you can use the content elements in your own back end modules
such as for example the news or calendar core extension do.

This allows you to provide the whole flexibility you have within articles in
other parts of your application with ease.

For the purpose of this cookbook entry we take the news module as reference.

All you need to do are the following three steps:

1. Define `tl_content` as a child table of your current DCA

    ``` {.php}
    // system/modules/news/dca/tl_news.php
    
    /**
     * Table tl_news
     */
    $GLOBALS['TL_DCA']['tl_news'] = array
    (
        // Config
        'config' => array
        (
            [...]
            'ctable'                      => array('tl_content'),
    ```

2. Dynamically set the parent table in the DCA of `tl_content`

    ``` {.php}
    // system/modules/news/dca/tl_content.php
    
    /**
     * Dynamically add parent table
     */
    if (\Input::get('do') == 'news')
    {
        $GLOBALS['TL_DCA']['tl_content']['config']['ptable'] = 'tl_news';
    }
    ```

3. Route your edit link to the `tl_content` table

    Instead of

    ``` {.php}
    // system/modules/news/dca/tl_news.php
    'edit' => array
    (
        'label'               => &$GLOBALS['TL_LANG']['tl_news']['edit'],
        'href'                => 'act=edit',
        'icon'                => 'edit.gif'
    ),
    ```

    you should now use

    ``` {.php}
    // system/modules/news/dca/tl_news.php
    'edit' => array
    (
        'label'               => &$GLOBALS['TL_LANG']['tl_news']['edit'],
        'href'                => 'table=tl_content',
        'icon'                => 'edit.gif'
    ),
    ```

That's it. You can now use content elements within your own DCA.


## Fetching the content elements in your front end module

For your convenience, Contao ships with a helper method within the
`ContentModel` so you can easily fetch all your related content elements:

``` {.php}
$strContent = '';

$objElements = \ContentModel::findPublishedByPidAndTable($objNews->id, 'tl_news');

if ($objElements !== null)
{
    while ($objElements->next())
    {
        // Controller::getContentElement()
        $strContent .= $this->getContentElement($objElements->id);
    }
}

// Now contains a string of all generated content elements
echo $strContent;
```
