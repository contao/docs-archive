# Die Toggle-Funktion in eigenen Erweiterungen nutzen

Die Toggle-Funktion wird in Contao in der Regel durch ein grünes Auge 
symbolisiert und dient dem schnellen Ein- und Ausblenden von Datensätzen 
über die Listenansicht.

Es sind vier Schritte nötig: 

1. Einfügen eines Feldes in die Datenbank und DCA
2. Einfügen einer Aktion in den DCA
3. Erstellen einer Methode, die das Icon gemäß dem Status anzeigt
4. Erstellen einer Methode, die den Status in der Datenbank setzt


## 1. Einfügen eines Feldes in die Datenbank und DCA

Falls noch nicht vorhanden, muss als erstes ein Feld in der Tabelle
und eine entsprechende Konfiguration im DCA angelegt werden. Seit
Contao 3 wird keine `database.sql` mehr benötigt. Die SQL-Definitionen
werden direkt im DCA implementiert.

```php
$GLOBALS['TL_DCA']['tl_example']['fields']['published'] = array
(
    'label'               => &$GLOBALS['TL_LANG']['tl_example']['published'],
    'exclude'             => true,
    'filter'              => true,
    'inputType'           => 'checkbox',
    'sql'                 => "char(1) NOT NULL default ''"
);
```

*`tl_example` ist durch den Namen der Tabelle zu ersetzen!*


## 2. Einfügen einer Aktion in das DCA
```php
$GLOBALS['TL_DCA']['tl_example']['list']['operations']['toggle'] = array
(
    'label'               => &$GLOBALS['TL_LANG']['tl_example']['toggle'],
    'icon'                => 'visible.gif',
    'attributes'          => 'onclick="Backend.getScrollOffset();return AjaxRequest.toggleVisibility(this,%s)"',
    'button_callback'     => array('tl_example', 'toggleIcon')
);
```

*`tl_example` ist durch den Namen der Tabelle zu ersetzen!*


## 3. Erstellen einer Methode, die das Icon gemäß dem Status setzt

Für das in Punkt 2 definierte `button_callback` muss auch eine Methode
erstellt werden, die das Icon anhand des Status setzt. Hierfür wird eine
eigene Klasse angelegt. Wenn bereits eine Klasse mit anderen Callbacks
o.ä. vorhanden ist, können die Methoden auch dort eingefügt werden.

```php
class tl_example
{
    /**
     * Ändert das Aussehen des Toggle-Buttons.
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

In der Methode `toggleIcon` wird die Methode `toggleVisibility` aufgerufen,
wenn ein entsprechender URL-Parameter vorhanden ist. Dies funktioniert sowohl
per Ajax als auch als Javascript-Fallback-Link.

```php
/**
 * Toggle the visibility of an element
 * @param integer
 * @param boolean
 */
public function toggleVisibility($intId, $blnPublished)
{
    // Check permissions to publish
    if (!$this->User->isAdmin && !$this->User->hasAccess('tl_example::published', 'alexf'))
    {
        $this->log('Not enough permissions to show/hide record ID "'.$intId.'"', 'tl_example toggleVisibility', TL_ERROR);
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
    $this->Database->prepare("UPDATE tl_example SET tstamp=". time() .", published='" . ($blnPublished ? '' : '1') . "' WHERE id=?")
        ->execute($intId);
    $this->createNewVersion('tl_example', $intId);
}
```
