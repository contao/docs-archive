## Den Safe Mode Hack verwenden

Eventuell haben Sie beim Aufruf des Contao-Installtools die Mitteilung erhalten,
dass die lokale Konfigurationsdatei nicht beschreibbar ist.

![](images/localconfig-not-writable.jpg?raw=true)


### Dateizugriffsrechte

Die Bezeichnung "Safe Mode Hack" ist eigentlich nicht korrekt, da sie
impliziert, dass das Problem durch den PHP safe_mode verursacht würde.
Tatsächlich wird es jedoch von unzureichenden Dateizugriffsrechten verursacht
und tritt auch bei deaktiviertem safe_mode auf, daher sollte es richtiger "File
Permission Hack" heißen.

PHP als Apache-Modul läuft normalerweise als Benutzer `wwwrun`, `www-data` oder
`nobody`, wohingegen die Dateien, die Sie per FTP hochgeladen haben, Ihrem
Benutzer (z.B. `web4` oder `ab5678`) gehören. Der Server verweigert Benutzern
grundsätzlich den Zugriff auf fremde Dateien und macht auch für das PHP-Skript
Contao keine Ausnahme.


#### FTP für Dateioperationen verwenden

Um das Rechteproblem zu umgehen, baut Contao eine FTP-Verbindung auf und legt
die Ressourcen unter dem FTP-Benutzer an. Sie müssen dafür nur Ihre
FTP-Zugangsdaten im Installtool eintragen. Achten Sie dabei besonders auf den
korrekten relativen Pfad vom FTP-Basisordner zum Contao-Verzeichnis (z.B.
`html/`, `public_html/` oder `httpdocs/`).

Ein paar wenige Verzeichnisse benötigen trotz Safe Mode Hack Schreibrechte, weil
PHP direkt auf sie zugreift:

* `assets/images`
* `assets/images/*`
* `system/logs`
* `system/tmp`

Die Schreibrechte (CHMOD 777) werden vom Installtool automatisch gesetzt und
müssen in der Regel nicht manuell nachgearbeitet werden. Falls dies doch einmal
notwendig sein sollte, passen Sie bitte **nur diese drei Verzeichnisse** an –
auch wenn Sie in einem Tutorial oder dem Contao-Forum etwas anderes gelesen
haben sollten!
