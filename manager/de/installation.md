# Contao Manager installieren


## Anforderung Hosting / Systemvoraussetzungen
Die Voraussetzungen entsprechen denen von Contao 4. Ein Kompatibilitätstest kann mit dem Contao Check durchgeführt werden.

**Weitere Daten einfügen?!**


## Konfiguration Hosting
Die Domain darf nicht auf das Root-Verzeichnis zeigen, sondern auf das
Verzeichnis `web`.

**Beispiel:**
meinedomain.de zeigt auf das Verzeichnis www/meinedomain/web

Eine Konfigurtaion mit Unterverzeichnissen ist nicht möglich. Pro Installation
wird eine (Sub)Domain benötigt.


## Download
Der Contao Manager besteht aus einer einzigen phar-Datei. Diese kann über
[contao.org][1] heruntergeladen werden.


## Entpacken und auf Webserver laden
Nach erfolgreichem Download muss die Datei entpackt werden. Sie sollten jetzt
eine Datei `contao-manager.phar.php` haben.
Diese wird per FTP auf den Webserver in das Verzeichnis `web` geladen. 


## Contao Manager aufrufen
Anschließend rufen Sie mit Ihrem Browser die Domain
`http://www.meinedomain.de/contao-manager.phar.php` auf.
Sie sollten nun den Willkommen-Screen des Contao Managers sehen.


## Grundkonfiguration
Bevor Sie nun Contao installieren, muss der Manager selbst konfiguriert werden.
Legen Sie dazu einen neuen Benutzer an, indem Sie Benutzernamen und ein Passwort
vergeben.
Das Passwort ist unabhängig von der späteren Contao Installation. Bitte nötiren
Sie sich die Zugangsdaten.

Der Contao Manager benötigt keine eigene Datenbank.
Die Konfiguration wird in mehreren Dateinen im Unterordner `contao-manager`
gespeichert.


## PHP binary - Experten Einstellungen
Der Contao Manager versucht automatisch die PHP-Version zu erkennen.
Leider ist das nicht immer möglich, deswegen sollten Sie die Einstellung noch
einmal prüfen.
Klicken Sie wenn nötig dazu einmal auf das Zahnradsymbol neben dem
Install-Button.

Ein Liste mit bekannten Hosting-Konfigurationen finden Sie hier:
**Liste Hosting PHP binaris? **

Nun können Sie die [Contao Installation](installation-contao.md) starten


[1]: https://contao.org/de/download.html
