# Contao Manager installieren

## Anforderung Hosting / Systemvoraussetzungen
Die Voraussetzungen entsprechen denen von Contao 4. Ein Kompatibilitätstest kann mit dem Contao Check durchgeführt werden.

**Weitere Daten einfügen?!**

## Konfiguration Hosting
Die Domain darf nicht auf das Root-Verzeichnis zeigen, sondern auf das Verzeichnis `web`.

**Beispiel:**
meinedomain.de zeigt auf das Verzeichnis www/meinedomain/web

Eine Konfigurtaion mit Unterverzeichnissen ist nicht möglich. Pro Installation wird eine (Sub)Domain benötigt.

## Download
Der Contao Manager besteht aus einer einzigen phar-Datei. Diese kann über contao.org (Link ergänzen) heruntergeladen werden.

## Entpacken und auf Webserver laden
Nach erfolgreichem Download muss die Datei entpackt werden. Sie sollten jetzt eine Datei `contao-manager.phar.php` haben.
Diese wird per FTP auf den Webserver in das Verzeichnis `web` geladen. 

## Contao Manager aufrufen
Anschließend rufen Sie mit Ihrem Browser die Domain `http://www.meinedomain.de/contao-manager.phar.php` auf.
Sie sollten nun den Willkommen-Screen des Contao Managers sehen.

## Grundkonfiguration
Bevor Sie nun Contao installieren, muss der Manager selbst konfiguriert werden. Legen Sie dazu einen neuen Benutzer an, indem Sie Benutzernamen und ein Passwort vergeben.
Das Passwort ist unabhängig von der späteren Contao Installation. Bitte nötiren Sie sich die Zugangsdaten.

Der Contao Manager benötigt keine eigene Datenbank.
Die Konfiguration wird in mehreren Dateinen im Unterordner `contao-manager` gespeichert.

## PHP binary - Experten Einstellungen
Der Contao Manager versucht automatisch die PHP-Version zu erkennen.
Leider ist das nicht immer möglich, deswegen sollten Sie die Einstellung noch einmal prüfen.
Klicken Sie wenn nötig dazu einmal auf das Zahnradsymbol neben dem Install-Button.

Ein Liste mit bekannten Hosting-Konfigurationen finden Sie hier:
**Liste Hosting PHP binaris? **

## Contao Installation starten
Nun kann Contao installiert werden. Dazu wählen Sie die gewünschte Version aus und klicken auf den Install-Button. 
Die Installation kann nun mehrere Minuten in Anspruch nehmen. Details zur Installation können Sie sich durch Klick auf *Show Console Output* angezeigt werden.

## Contao Install Tool aufrufen
Sobald der Contao Manager alle Pakete installiert hat, klicken SIe auf den Button 'Install Tool' und rufen dieses auf.
Folgenden Sie den Anweisungen und vergeben ein zunächst ein Passwort. Anschließend geben Sie die Daten für Ihre Datenbankverbindung ein und klicken auf aktualisieren.
Zum Schluss legen Sie noch ein Administratorkonto für das Contao Backend an.
Sie können das Install Tool nun schließen und beim Contao Manager auf "Confirm & Close" klicken.

Sie haben nun erfolgreich Contao über den Contao Manager installiert.
