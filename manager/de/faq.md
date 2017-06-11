# Häufige Fragen - FAQ

Hier finden Sie eine Übersicht über häufige Fragen zum Contao Manager.


## Wie kann man den Contao Manager aktualisieren?
Grundsätzlich ist ein manuelles Update nicht nötig. Der CM führt täglich
automatisch im Hintergrund eine Prüfung durch. Sollte eine neue Version
verfügbar sein, aktualisiert sich der Manager selbst.

Bei Problemen können Sie jederzeit die aktuellste `contao-manager.phar.php`
herunterladen und diese manuell per FTP hochladen und ersetzen.


## Contao Manager Zugangsdaten vergessen
Um Ihr Passwort zurückzusetzen, müssen Sie sich per FTP mit Ihrem Server
verbinden.

Löschen Sie im Verzeichnis `contao-manager` die Datei `users.json`.

Rufen Sie nun den Contao Manager (`contao-manager.phar.php`) erneut auf und
legen einen neuen Admin-User an.


## Kann der Contao Manager zu einer bestehenden Installation hinzugefügt werden?
Ja, wenn Sie eine Contao 4 Installation in der Managed Edition verwenden, dann
kann der CM nachinstalliert werden. Dazu einfach die `contao-manager.phar.php`
in das Verzeichnis `web` laden.

Der Manager erkennt bei der Grundinstallation, dass bereits Contao installiert
ist.