# Installation

Die folgenden Abschnitte erklären die Installation und Aktualisierung von
Contao. Sie lernen wie man das Contao-Installtool verwendet, wie man eine
Installation per FTP synchronisiert, wie man den Safe Mode Hack einrichtet und
wie man einen Webserver für Contao konfiguriert.


## Contao installieren

Laden Sie sich zunächst das [aktuelle Contao-Archiv][1] herunter und entpacken
Sie es auf Ihrem lokalen Rechner. Verschieben Sie die Dateien in das
`htdocs`-Verzeichnis Ihrer XAMPP-Installation oder kopieren Sie sie mit einem
FTP-Programm (z.B. [WinSCP][2]) auf Ihren Server. Der Basisordner heißt
wahrscheinlich `htdocs`, `httpdocs`, `html` oder `public_html`.

Wenn Sie SSH-Zugriff auf den Server haben, können Sie alternativ folgende
Befehle verwenden:

``` {.bash}
curl -L http://download.contao.org | tar -xzp
```


### Das Contao-Installtool

Um das Contao-Installtool aufzurufen, hängen Sie einfach `/contao/install.php`
an die URL Ihrer Contao-Installation an. Beachten Sie, dass das Installtool mit
einem Passwort gegen Brute Force-Attacken geschützt ist und gesperrt wird, wenn
dreimal hintereinander ein falsches Passwort eingegeben wurde. Um diese Sperre
aufzuheben, öffnen Sie die Datei `system/config/localconfig.php` in einem
Texteditor, finden Sie die folgende Zeile und setzen Sie sie auf `0`.

``` {.php}
$GLOBALS['TL_CONFIG']['installCount'] = 0; // Hebt die automatische Sperre auf
```


#### Datenbankverbindung herstellen

Melden Sie sich an der Administrationsoberfläche Ihres Servers (z.B. "Plesk"
oder "Cpanel") an und erstellen Sie eine neue Datenbank für Contao. Geben Sie
die Zugangsdaten im Contao-Installtool ein und beachten Sie die abweichende
Schreibweise `UTF8` anstatt `UTF-8` in MySQL!


#### Tabellen aktualisieren

Contao prüft bei der Installation die Tabellen der Datenbank und gibt eine
Liste empfohlener Änderungen aus, wenn diese nicht aktuell sind. Lesen Sie diese
Empfehlungen aufmerksam, denn Contao kennt nur seine eigenen Tabellen und wird
versuchen, vermeintlich nicht benötigte Tabellen anderer Programme
"aufzuräumen". Bestätigen Sie die Änderungen durch Anklicken der "Datenbank
aktualisieren"-Schaltfläche.


#### Ein Template importieren

Ein Template ist eine vorkonfigurierte Webseite, die eine beispielhafte
Seitenstruktur und verschiedene Stylesheets zur Formatierung der Contao
Core-Module und -Inhaltselemente enthält. Das Standardtemplate heißt "Music
Academy". Um es zu importieren, wählen Sie den Eintrag `example_website.sql` aus
dem Drop-Down-Menü und klicken Sie auf die "Template importieren"-Schaltfläche.

**Beim Import eines Templates werden bestehende Daten überschrieben!**


#### Administrator-Konto erstellen

Wenn Sie kein Template importiert haben, müssen Sie ein Administrator-Konto
erstellen, damit Sie sich am Contao-Backend anmelden können. Danach ist der
Installationsprozess abgeschlossen. Der Link unten rechts leitet Sie zur
Backend-Anmeldung weiter. Wenn Sie die Beispielwebseite importiert haben, können
Sie sich dort als Benutzer "k.jones" mit dem Passwort "kevinjones" anmelden.


### Suchmaschinenfreundliche URLs verwenden

Wenn Sie einen Apache-Webserver haben und mod_rewrite verwenden dürfen, können
Sie Contao dazu veranlassen, suchmaschinenfreundliche URLs zu generieren, die
wie statische HTML-Seiten aussehen. Die dazu benötigten Rewrite-Regeln sind in
der `.htaccess.default`-Datei im Contao-Verzeichnis gespeichert. Benennen Sie
diese Datei um in `.htaccess`, damit sie vom Apache-Server erkannt wird, und
rufen Sie anschließend das Modul "Einstellungen" im Contao-Backend auf. Wählen
Sie die Option "URLs umschreiben" in der Gruppe "Frontend-Einstellungen" aus und
speichern Sie Ihre Änderungen. Contao generiert jetzt statische URLs wie z.B.
`home.html` anstatt `index.php?id=12`.


## Den Safe Mode Hack verwenden

Eventuell haben Sie beim Aufruf des Contao-Installtools die Mitteilung erhalten,
dass die lokale Konfigurationsdatei nicht beschreibbar ist.

![](https://raw.github.com/contao/docs/2.11/manual/de/images/localconfig-not-writable.jpg)


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

* `system/html`
* `system/logs`
* `system/tmp`

Die Schreibrechte (CHMOD 777) werden vom Installtool automatisch gesetzt und
müssen in der Regel nicht manuell nachgearbeitet werden. Falls dies doch einmal
notwendig sein sollte, passen Sie bitte **nur diese drei Verzeichnisse** an –
auch wenn Sie in einem Tutorial oder dem Contao-Forum etwas anderes gelesen
haben sollten!


## Manuelles Update

Bei der manuellen Aktualisierung einer Contao-Installation können Sie entweder
das komplette Contao-Archiv auf den Server übertragen (Dateien ersetzen) oder
nur die geänderten Dateien hochladen (Dateien synchronisieren). In jedem Fall
sollten Sie vorher folgende Dateien und Ordner sichern - nur für den Fall, dass
ein Fehler auftritt oder Sie sie versehentlich überschreiben:

* `system/config/dcaconfig.php`
* `system/config/initconfig.php`
* `system/config/langconfig.php`
* `system/config/localconfig.php`
* `templates/*`
* `tl_files/*`

Dieses Backup umfasst Ihre lokale Konfiguration, eventuell angepasste Templates
sowie die hochgeladenen Dateien.


### Dateien ersetzen

Die Dateien einer Contao-Installation zu ersetzen ist relativ simpel. Übertragen
Sie einfach das Contao-Archiv auf Ihren Server oder entpacken Sie es auf Ihrem
lokalen Rechner und kopieren Sie die Dateien anschließend mit einem FTP-Programm
(wir empfehlen [WinSCP][2]). Danach stellen Sie die Dateien aus dem Backup
wieder her und entfernen eventuelle Überbleibsel vorheriger Contao-Versionen.

**Achtung:** Wenn Sie Third-Party-Erweiterungen installiert haben, müssen Sie
diese ebenfalls sichern und nach dem Update wiederherstellen oder darauf achten,
sie gar nicht erst zu überschreiben. Andernfalls müssen diese Module neu
installiert werden, was bei einigen Erweiterungen zu Datenverlust führen kann!


### Dateien synchronisieren

Um eine Contao-Installation zu synchronisieren, können Sie entweder das [Unix
Diff-Programm][3] oder einen FTP-Client verwenden. Unix-Utilities werden
normalerweise nur von Serveradministratoren verwendet, daher werden sie hier
nicht erklärt. Um Dateien per FTP zu synchronisieren, öffnen Sie WinSCP und
verbinden Sie sich mit dem Server. Erstellen Sie ein Backup der oben genannten
Dateien und navigieren Sie dann zum Contao-Verzeichnis und klicken Sie auf die
"Dateien synchronisieren"-Schaltfläche.

![](https://raw.github.com/contao/docs/2.11/manual/de/images/synchronization-options.jpg)

Treffen Sie Ihre Auswahl wie in der Abbildung und wählen Sie unbedingt die
Option "Änderungsvorschau" aus, damit Sie die zu aktualisierenden Dateien noch
einmal prüfen können. Bestätigen Sie danach die Einstellungen im Vorschaufenster
und achten Sie besonders auf die zu löschenden Ressourcen! Klicken Sie "OK", um
den Synchronisationsvorgang zu starten.

![](https://raw.github.com/contao/docs/2.11/manual/de/images/synchronization-confirmation.jpg)


### Die Datenbank aktualisieren

Nachdem Sie die Contao-Dateien aktualisiert haben, müssen Sie noch die Datenbank
auf den neuesten Stand bringen. Diese Arbeit übernimmt das Contao-Installtool
für Sie. Geben Sie Ihr Passwort ein, scrollen Sie bis zum Datenbank-Abschnitt
und bestätigen Sie die Änderungen.


## Live Update Service

Der Contao Live Update-Service ist ein kommerzielles Contao Add-on von [iNet
Robots][4], der Firma des Contao-Gründers und Kernentwicklers, Leo Feyer. Es
ermöglicht die Aktualisierung Ihrer Installation mit wenigen Klicks im Backend,
ohne ein Contao-Archiv herunterzuladen oder die Dateien mit einem FTP-Programm
zu synchronisieren.

[Eine Contao Live Update ID bestellen][5]

Das Live Update umfasst folgende Funktionen:

* Beliebige Up- und Downgrades auf alle Contao-Versionen
* Automatisches Backup der Datenbank vor dem Update
* Individuelle Prüfung und Vervollständigung der Contao-Installation
* Vergleich der angepassten Templates mit den Originaldateien


### Versionsauswahl

![](https://raw.github.com/contao/docs/2.11/manual/de/images/live-update-1.jpg)


### Template-Unterschiede

![](https://raw.github.com/contao/docs/2.11/manual/de/images/live-update-2.jpg)


### Fehlersuche

99% aller Live Update-Probleme sind auf unzureichende Datei-Zugriffsrechte
zurück zu führen. Contao benötigt Schreibrechte, um Dateien und Ordner zu
verwalten, daher sollten Sie als erstes Ihre Serverkonfiguration prüfen und
sicherstellen, dass der Safe Mode Hack **so wie in diesem Handbuch beschrieben**
konfiguriert ist!


#### Support erhalten

Wenn Sie Probleme bei der Aktivierung Ihrer Live Update ID haben, wenden Sie
sich bitte an den [iNet Robots-Support][6]. Bei Problemen mit dem Safe Mode Hack
oder der Benutzung von Contao, wählen Sie bitte eine passende Support-Option auf
der [Support-Seite][7].


## Eine Installation umziehen

Der Umzug einer Contao-Installation von einem lokalen Server auf einen
Live-Server ist nicht viel anders als eine neue Installation, außer dass Sie die
Dateien Ihrer lokalen Installation statt denen des Contao-Archivs sowie einen
SQL-Dump Ihrer lokalen Datenbank verwenden.


### Dateien kopieren

Öffnen Sie Ihr FTP-Programm, verbinden Sie sich mit dem Zielserver und
übertragen Sie alle Dateien Ihrer lokalen Contao-Installation.


### Datenbank exportieren

Ein MySQL-Dump lässt sich am einfachsten mit der Datenbankverwaltung
"phpMyAdmin" erstellen. Als Serveradministrator können Sie natürlich auch das
Programm `mysqldump` verwenden. Melden Sie sich an "phpMyAdmin" an, wählen Sie
die zu exportierende Datenbank und klicken Sie auf die "Export"-Schaltfläche im
oberen Menü. Um Kompatibilitätsprobleme zwischen verschiedenen MySQL-Versionen
zu minimieren `,ist es wichtig, die Einstellungen für den Export gemäß des
folgenden Screenshots anzupassen:

![](https://raw.github.com/contao/docs/2.11/manual/de/images/sql-export.jpg)


### Datenbank importieren

Öffnen Sie "phpMyAdmin" auf dem Zielserver an und erstellen Sie eine neue
Datenbank für Contao. Je nach Serverkonfiguration ist das eventuell nur über die
Verwaltungsoberfläche (z.B. "Plesk" oder "Cpanel") möglich. Wählen Sie die neue
leere Datenbank aus und klicken Sie auf die "Import"-Schaltfläche im oberen
Menü. Laden Sie dann den SQL-Dump der lokalen Datenbank hoch und starten Sie den
Import.

![](https://raw.github.com/contao/docs/2.11/manual/de/images/sql-import.jpg)


### Datenbank-Konfiguration anpassen

Als letztes öffnen Sie das Contao-Installtool der neuen Installation (das
Passwort ist dasselbe wie für Ihre lokale Installation) und passen wenn nötig
die Datenbank-Zugangsdaten an. Danach können Sie sich wie gewohnt mit Ihrem
Benutzernamen im Backend anmelden.


## Den Live-Server konfigurieren

In diesem Kapitel geht es nicht darum, den Apache-Dienst zu installieren oder
PHP zu kompilieren, was auf einem Shared-Hosting-Server ohnehin nicht möglich
ist. Stattdessen wird erklärt, wie man die Contao-Systemvoraussetzungen prüft
und PHP 5 aktiviert.


### Contao-Systemvoraussetzungen

Contao benötigt einen Webserver wie Apache oder IIS mit PHP- und MySQL-Support.
PHP muss mindestens in der Version 5.2.7 vorliegen und MySQL in der Version 4.1,
wobei wir für eine bessere Performance MySQL 5 empfehlen. Außerdem benötigen
Sie die PHP-Erweiterungen "GDlib" (Bildbearbeitung) und "SOAP" (Extension
Repository) sowie optional "mbstring" (internationale Zeichen) und "mcrypt"
(Verschlüsselung). Contao wurde erfolgreich in allen modernen Browsern wie
Firefox (ab Version 2) oder Internet Explorer (ab Version 7) getestet.


### Der Contao-Check

Laden Sie den Contao-Check herunter und finden Sie heraus, ob Ihr Server die
Contao-Systemvoraussetzungen erfüllt. Der Contao-Check prüft, ob Sie das
Extension Repository und das Live Update nutzen können und ob Sie den Safe Mode
Hack benötigen oder nicht. Je nach Systemkonfiguration können Sie mit Hilfe des
Web-Installers eine neue Contao-Installation aufsetzen oder eine bestehende
Installation prüfen.

![](https://raw.github.com/contao/docs/2.11/manual/de/images/contao-check.jpg)

Entpacken Sie die Zip-Datei, übertragen Sie den Ordner
`check` in Ihr Contao-Verzeichnis und öffnen Sie ihn in einem Browser.

[Den Contao-Check herunterladen][8] | [Zum Projekt auf GitHub][9]


### Provider-spezifische Einstellungen

Es gibt ein paar wenige große Internet Service Provider, die spezielle
Einstellungen für den Betrieb von Contao erfordern. Zum Glück sind sie nur die
Ausnahme von der Regel. Die Provider-spezifische Einstellungen finden Sie im
[Contao-Forum][10]. Sorgenfreies Contao-Hosting erhalten Sie bei den [Contao
Hosting-Partnern][11].


[1]: https://contao.org/de/download.html
[2]: http://www.winscp.com
[3]: http://de.wikipedia.org/wiki/Diff
[4]: http://www.inetrobots.com
[5]: http://www.inetrobots.com/shop/product_info.php?info=p12_Live-Update-ID.html
[6]: http://www.inetrobots.com/kontakt.html
[7]: https://contao.org/de/support.html
[8]: https://github.com/contao/check/zipball/master
[9]: https://github.com/contao/check
[10]: https://community.contao.org/de/forumdisplay.php?67-Erfahrungen-mit-Webhostern
[11]: https://contao.org/de/partners.html?search=services&for=partner_hosting
