# Inhaltselemente in deiner eigenen Erweiterung nutzen

Seit Contao 3.0 gibt es die Möglichkeit, die Inhaltselemente auch in eigenen
Backend-Modulen wie bspw. bei den Nachrichten oder Events zu nutzen.
	
Das ermöglicht es, die gesamte Flexibilität welche Inhaltselemente in Artikeln
bieten, auch in anderen Teilen der Applikation zu nutzen.

Für dieses Beispiel dient uns das Nachrichten-Modul als Referenz.

Alles was du machen musst, sind die folgenden drei Schritte:

1. Definiere `tl_content` als Kindtabelle deines aktuellen DCA's

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

2. Setze die Elterntabelle von `tl_content` dynamisch

    ``` {.php}
    // system/modules/news/dca/tl_content.php
    
    /**
     * Dynamically add the parent table
     */
    if (\Input::get('do') == 'news')
    {
        $GLOBALS['TL_DCA']['tl_content']['config']['ptable'] = 'tl_news';
    }
    ```

3. Leite den editieren-Link zur `tl_content` Table

    Anstelle von

    ``` {.php}
    'edit' => array
    (
        'label'               => &$GLOBALS['TL_LANG']['tl_news']['edit'],
        'href'                => 'act=edit',
        'icon'                => 'edit.gif'
    ),
    ```

    solltest du Folgendes nutzen:

    ``` {.php}
    // system/modules/news/dca/tl_news.php
    'edit' => array
    (
        'label'               => &$GLOBALS['TL_LANG']['tl_news']['edit'],
        'href'                => 'table=tl_content',
        'icon'                => 'edit.gif'
    ),
    ```
4. Füge `tl_content` zu den erlaubten Tabellen hinzu

    ``` {.php}
    // system/modules/news/config/config.php
    $GLOBALS['BE_MOD']['content']['news'] = array
    (
    	'tables' 		=> array('tl_news', 'tl_content')
    )
    ```

Das war's. Du kannst jetzt Inhaltselemente in deinem eigenen DCA nutzen.


## Wie hole ich mir die Inhaltselemente in meinem Frontend-Modul?

Das `ContentModel` kommt mit einer Hilfsmethode, welche das einfache Laden von
Inhaltselementen ermöglicht:

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

// Enthält jetzt einen String mit allen generierten Inhaltselementen
echo $strContent;
```
