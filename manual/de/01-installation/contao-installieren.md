## Contao installieren

Laden Sie sich zunächst das [aktuelle Contao-Archiv][1] herunter und entpacken
Sie es auf Ihrem lokalen Rechner. Verschieben Sie die Dateien in das
`htdocs`-Verzeichnis Ihrer XAMPP-Installation oder kopieren Sie sie mit einem
FTP-Programm (z.B. [WinSCP][2]) auf Ihren Server. Stellen Sie sicher dass auch
die Datei `.htaccess.default` hochgeladen wird und benennen Sie diese danach
auf `.htaccess` um. Der Basisordner heißt wahrscheinlich `htdocs`, `httpdocs`,
`html` oder `public_html`.

Wenn Sie SSH-Zugriff auf den Server haben, können Sie alternativ folgende
Befehle verwenden:

```bash
curl -L http://download.contao.org | tar -xzp
```


### Das Contao-Installtool

Um das Contao-Installtool aufzurufen, hängen Sie einfach `/contao/install.php`
an die URL Ihrer Contao-Installation an. Beachten Sie, dass das Installtool mit
einem Passwort gegen Brute Force-Attacken geschützt ist und gesperrt wird, wenn
dreimal hintereinander ein falsches Passwort eingegeben wurde. Um diese Sperre
aufzuheben, öffnen Sie die Datei `system/config/localconfig.php` in einem
Texteditor, finden Sie die folgende Zeile und setzen Sie sie auf `0`.

```php
$GLOBALS['TL_CONFIG']['installCount'] = 0; // Hebt die automatische Sperre auf
```


#### Datenbankverbindung herstellen

Melden Sie sich an der Administrationsoberfläche Ihres Servers (z.B. "Plesk"
oder "cPanel") an und erstellen Sie eine neue Datenbank für Contao. Geben Sie
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
Core-Module und -Inhaltselemente enthält.

Seit Version 3.2.11 ist die Beispiel-Webseite nicht mehr im Downloadpaket enthalten.
Abhängig von der eingesetzten Version kann die neue [*Contao Official Demo*][3]
oder die alte [*Music Academy*][4] als Erweiterung installiert werden.
Aufschluss über Kompatibilität gibt das Erweiterungsverzeichnis.

Vorgehen zur Installation der Demo:

1. Eine frische Contao Installation mit Admin-Account erstellen
2. Als Admin im Backend anmelden
3. Passende Erweiterung [über das Extension Repository][5] hinzufügen
4. Als Admin vom Backend abmelden
5. Installtool erneut aufrufen

Um ein Template zu importieren, wählen Sie den Eintrag aus dem Drop-Down-Menü
und klicken Sie auf die "Template importieren"-Schaltfläche.

> **Danger** Beim Import eines Templates werden bestehende Daten überschrieben!


#### Administrator-Konto erstellen

Wenn Sie kein Template importiert haben, müssen Sie ein Administrator-Konto
erstellen, damit Sie sich am Contao-Backend anmelden können. Danach ist der
Installationsprozess abgeschlossen. Der Link unten rechts leitet Sie zur
Backend-Anmeldung weiter. Wenn Sie die Beispielwebseite importiert haben, können
Sie sich dort als Benutzer "k.jones" mit dem Passwort "kevinjones" anmelden.


### Contao Demo installieren

Siehe *Vorgehen zur Installation der Demo* im Abschnitt *Ein Template importieren*
weiter oben.


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


[1]: https://contao.org/de/download.html
[2]: http://www.winscp.net
[3]: https://contao.org/de/extension-list/view/official_demo.de.html
[4]: https://contao.org/de/extension-list/view/music_academy.de.html
[5]: ../05-systemadministration/erweiterungen.html#erweiterungskatalog
