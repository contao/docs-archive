# Die Toggle-Funktion in eigenen Erweiterungen nutzen

Die Toggle-Funktion wird in Contao in der Regel durch ein grüne Auge 
symbolisiert und dient dem schnellen ein- und ausblenden von Datensätzen 
über die Listenansicht.

Es sind drei Schritte nötig: 

1. Einfügen einer Aktion in den DCA
2. Einfügen eines Feldes in die Datenbank und DCA
2. Erstellen einer Methode, die das Icon gemäß dem Status setzt
3. Erstellen einer Methode, die den Status in der Datenbank setzt


## 1. Einfügen einer Aktion in den DCA
```{.php}
$GLOBALS['TL_DCA']['tl_test']['list']['operations']['toggle'] = array
(
    'label'               => &$GLOBALS['TL_LANG']['tl_test']['toggle'],
    'icon'                => 'visible.gif',
    'attributes'          => 'onclick="Backend.getScrollOffset();return AjaxRequest.toggleVisibility(this,%s)"',
    'button_callback'     => array('tl_test', 'toggleIcon')
);
```

*`tl_test` ist durch den Namen der Tabelle zu ersetzen!*


## 2. Einfügen eines Feldes in die Datenbank und DCA

Als erstes wird ein Feld in der Tabelle und eine entsprechende Konfiguration 
im DCA angelegt. Seit Contao 3 wird keine `database.sql` mehr benötigt. Die 
SQL-Definitionen werden direkt im DCA implementiert.

```{.php}
$GLOBALS['TL_DCA']['tl_example']['list']['operations']['published'] = array
(
    'label'                => &$GLOBALS['TL_LANG']['tl_test']['published'],
     'exclude'             => true,
     'filter'              => true,
     'inputType'           => 'checkbox',
     'sql'                 => "char(1) NOT NULL default ''"
);
```

*`tl_example` ist durch den Namen der Tabelle zu ersetzen!*


## 3. Erstellen einer Methode, die das Icon gemäß dem Status setzt

Nun wird eine Methode erstellt, die das Icon anhand des Status setzt. Hier für 
wird eine eigene Klasse angelegt. Wenn bereits eine Klasse mit anderen 
Callbacks o.ä. vorhanden ist, können die Methoden auch dort eingefügt werden.

```{.php}
class myClass
{
    /**
     * Aendert das Aussehen der Toggel-Buttons.
     * @param $row
     * @param $href
     * @param $label
     * @param $title
     * @param $icon
     * @param $attributes
     * @return string
     */
    public function toggleIcon($row, $href, $label, $title, $icon, $attributes)
    {
        $this->import('BackendUser', 'User');

        if (strlen($this->Input->get('tid')))
        {
            $this->toggleVisibility($this->Input->get('tid'), ($this->Input->get('state') == 0));
            $this->redirect($this->getReferer());
        }

        // Check permissions AFTER checking the tid, so hacking attempts are logged
        if (!$this->User->isAdmin && !$this->User->hasAccess('tl_example::published', 'alexf'))
        {
            return '';
        }

        $href .= '&amp;id='.$this->Input->get('id').'&amp;tid='.$row['id'].'&amp;state='.$row[''];

        if (!$row['published'])
        {
            $icon = 'invisible.gif';
        }

        return '<a href="'.$this->addToUrl($href).'" title="'.specialchars($title).'"'.$attributes.'>'.$this->generateImage($icon, $label).'</a> ';
    }
}
```


## 4. Erstellen einer Methode, die den Status in der Datenbank setzt

In der Methode `toggleIcon` wird die Methode `toggleVisibility` da diese über 
`$this->toggleVisibility()` aufgerufen wird, muss sie in der gleichen KLasse 
liegen. Die Klasse wird in dem Beilspiel nicht noch einmal 
aufgeführt.

```{.php}
/**
 * Toggle the visibility of an element
 * @param integer
 * @param boolean
 */
public function toggleVisibility($intId, $blnPublished)
{
    // Check permissions to edit
    $this->Input->setGet('id', $intId);
    $this->Input->setGet('act', 'toggle');

    // Check permissions to publish
    if (!$this->User->isAdmin && !$this->User->hasAccess('tl_example::published', 'alexf'))
    {
        $this->log('Not enough permissions to show/hide content element ID "'.$intId.'" tl_example toggleVisibility', 'tl_content toggleVisibility', TL_ERROR);
        $this->redirect('contao/main.php?act=error');
    }

    $this->createInitialVersion('tl_example', $intId);

    // Trigger the save_callback
    if (is_array($GLOBALS['TL_DCA']['tl_example']['fields']['published']['save_callback']))
    {
        foreach ($GLOBALS['TL_DCA']['tl_example']['fields']['published']['save_callback'] as $callback)
        {
            $this->import($callback[0]);
            $blnPublished = $this->$callback[0]->$callback[1]($blnPublished, $this);
        }
    }

    // Update the database
    $this->Database->prepare("UPDATE tl_test SET tstamp=". time() .", published='" . ($blnPublished ? '' : 1) . "' WHERE id=?")
        ->execute($intId);
    $this->createNewVersion('tl_example', $intId);
}
```
