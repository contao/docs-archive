# Häufige Fragen - FAQ

Hier finden Sie eine Übersicht über häufige Fragen zum Contao Manager.


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