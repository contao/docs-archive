## Konfiguration anpassen

Die Contao-Konfiguration ist in drei Bestandteile aufgeteilt: die
Systemkonfiguration, die DCA-Konfiguration und die Sprachkonfiguration. Das
globale Konfigurationsarray wird zur Laufzeit aus denjenigen Bestandteilen
zusammengesetzt, die für die Ausgabe einer Seite gebraucht werden. Um Zeit und
Arbeitsspeicher zu sparen, werden nicht benötigte Konfigurationsdateien dabei
übersprungen.


### Die Systemkonfiguration anpassen

Die Systemkonfiguration ist in den `config.php`-Dateien der verschiedenen
Contao-Module gespeichert. Änderungen können updatesicher in der Datei
`system/config/localconfig.php` hinterlegt werden. Die meisten Parameter werden
in den Backend-Einstellungen gesetzt und automatisch in die lokale
Konfigurationsdatei geschrieben, so dass Sie diese in der Regel nicht manuell
bearbeiten müssen.

```php
// Den Extension Creator abschalten
unset($GLOBALS['BE_MOD']['devtools']['extension']);

### INSTALL SCRIPT START ###
$GLOBALS['TL_CONFIG']['debugMode'] = false;
$GLOBALS['TL_CONFIG']['displayErrors'] = false;
```

Platzieren Sie Ihre Änderungen unbedingt oberhalb der Zeile `INSTALL SCRIPT
START`, da sie andernfalls automatisch entfernt werden. Und **speichern Sie Ihre
Einstellungen niemals in der Datei config.php**, da diese Datei bei
Aktualisierungen überschrieben werden kann!


### Die DCA-Konfiguration anpassen

Contao verwendet [Data Container Arrays][1] zur Speicherung von
Tabellen-Metadaten. Die Data Container-Konfiguration ist in den `dca`-Ordnern
der verschiedenen Contao-Module hinterlegt und kann in der Datei
`system/config/dcaconfig.php` updatesicher angepasst werden.

```php
// Firma zu einem Pflichtfeld in der Mitgliedertabelle machen
$GLOBALS['TL_DCA']['tl_member']['fields']['company']['eval']['mandatory'] =
true;

// Firmennamen dürfen nur alphanumerische Zeichen beinhalten
$GLOBALS['TL_DCA']['tl_member']['fields']['company']['eval']['rgxp'] = 'alnum';

// Nur Administratoren dürfen Include-Elemente verwenden
if (!BackendUser::getInstance()->isAdmin)
{
    unset($GLOBALS['TL_CTE']['includes']);
}
```

Wie Sie sehen, eignet sich die Datei `dcaconfig.php` hervorragend für kleinere
Anpassung der Contao-Konfiguration. Größere Änderungen sollten jedoch zur
besseren Übersicht in einem eigenen Modul gekapselt werden.


### Bezeichnungen und Übersetzungen anpassen

Bezeichnungen und Übersetzungen sind in den `languages`-Ordnern der
verschiedenen Contao-Module hinterlegt. Jede Sprache wird anhand ihres
[ISO-639-1 Sprachcodes][2] identifiziert. Änderungen können updatesicher in
der Datei `system/config/langconfig.php` gespeichert werden.

```php
// Eine Bezeichnung in allen Sprachen ändern
$GLOBALS['TL_LANG']['MSC']['goBack'] = '«';

// Eine Bezeichnung in einer bestimmten Sprache ändern
if ($GLOBALS['TL_LANGUAGE'] == 'de')
{
    $GLOBALS['TL_LANG']['tl_layout']['column'] = 'Bereich';
}
elseif ($GLOBALS['TL_LANGUAGE'] == 'fr')
{
    $GLOBALS['TL_LANG']['tl_layout']['column'] = 'Section';
}
```

Auch Sprachanpassungen können in einem eigenen Modul gekapselt werden, was ab
einer bestimmten Anzahl empfohlen ist.


[1]: 06-Data-Container-Arrays.md
[2]: http://en.wikipedia.org/wiki/List_of_ISO_639-1_codes