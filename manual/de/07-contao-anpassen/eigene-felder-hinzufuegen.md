## Eigene Felder hinzufügen

Nehmen wir an, Sie möchten die Mitgliedertabelle um eine Kundennummer
erweitern. Da das Hinzufügen eines Feldes mehr erfordert als nur das Ändern
einer einzelnen Datei, wird das Anlegen eines eigenen Moduls im Verzeichnis
`system/modules` empfohlen. Denken Sie daran, dass Module in alphabetischer
Reihenfolge geladen werden. Nennen Sie es also nicht `custom`, wenn Sie damit
die `news`-Erweiterung anpassen wollen.


### Die DCA-Konfiguration erweitern

Legen Sie die Datei `dca/tl_member.php` in Ihrem Modulordner an und fügen Sie
die Metadaten des neuen Feldes ein.
Seit Contao 3 werden außerdem auch die dazugehörigen Felder sowie deren 
Konfiguration für die Datenbank unter `sql` direkt mit angegeben. 

```php
// Anpassung der Palette
$GLOBALS['TL_DCA']['tl_member']['palettes']['default'] = str_replace
(
    'company',
    'customer_number,company',
    $GLOBALS['TL_DCA']['tl_member']['palettes']['default']
);

// Hinzufügen der Feld-Konfiguration
$GLOBALS['TL_DCA']['tl_member']['fields']['customer_number'] = array
(
    'label'     => &$GLOBALS['TL_LANG']['tl_member']['customer_number'],
    'exclude'   => true,
    'inputType' => 'text',
    'eval'      => array('mandatory'=>true, 'rgxp'=>'digit', 'maxlength'=>8),
    'sql'       => "varchar(8) NOT NULL default ''"
);
```

Falls Sie den obigen Code nicht verstehen, lesen Sie den Abschnitt über [Data
Container Arrays][1].

Nachdem Sie die Datei abgespeichert haben, müssen Sie die Datenbank 
aktualisieren. Dazu verwenden Sie das [Contao-Installtool][2].


### Eine Übersetzung hinzufügen

Erstellen Sie die Datei `languages/de/tl_member.php` in Ihrem Modulordner und
legen Sie die deutschen Bezeichnungen an:

```php
$GLOBALS['TL_LANG']['tl_member']['customer_number'] = array
(
    'Kundennummer',
    'Bitte geben Sie die 8-stellige Kundennummer ein.'
);
```

Jetzt können Sie in der Mitgliederverwaltung eine bis zu 8 Ziffern lange
Kundennummer eingeben. Wird das Feld nicht ausgefüllt oder enthält es
nicht-numerische Zeichen, gibt Contao beim Abschicken des Formulars eine
entsprechende Fehlermeldung aus.


[1]: ../06-data-container-arrays/README.md
[2]: ../01-installation/contao-installieren.md#das-contao-installtool