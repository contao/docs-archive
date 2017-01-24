## Contao installieren

Laden Sie sich zunächst das [aktuelle Contao-Archiv][1] herunter und entpacken
Sie es auf Ihrem lokalen Rechner. Verschieben Sie die Dateien in das
`htdocs`-Verzeichnis Ihrer XAMPP-Installation oder kopieren Sie sie mit einem
FTP-Programm (z.B. [WinSCP][2]) auf Ihren Server. Der Basisordner heißt 
wahrscheinlich `htdocs`, `httpdocs`, `html`, `public_html` oder `www`.

Wenn Sie SSH-Zugriff auf den Server haben, können Sie Contao auch direkt
über die Kommandozeile herunterladen, beispielsweise mit `curl`. Je nach
gewünschter Version ist die URL anzupassen.

Neuste Version von Contao (4.x):
```bash
curl -L http://download.contao.org | tar -xzp
```

<abbr title="Long Term Support">LTS</abbr>-Version von Contao (3.5):
```bash
curl -L http://download.contao.org/lts | tar -xzp
```

Eine bestimmte Version (z.B. 3.5.2):
```bash
curl -L http://download.contao.org/3.5.2 | tar -xzp
```


### Installation mit Composer

Mit Composer kann Contao über die [contao/standard-edition][3] installiert
werden.

Als Erstes muss [Composer verfügbar sein][4], welcher mit folgendem Befehl
auf einem macOS- oder Linux-System installiert werden kann:

```bash
curl -sS https://getcomposer.org/installer | php
sudo mv composer.phar /usr/local/bin/composer
```

Unter Windows erfolgt die Installation mittels dem [Installer][5].

Nun kann die Installation von Contao mit folgendem Befehl gestartet werden:

```bash
composer create-project contao/standard-edition <ziel>
```

Geben Sie als `<ziel>` den Ordner ein, in welchen die Contao-Dateien
installiert werden sollen. Wenn der Ordner nicht vorhanden ist, wird er
automatisch angelegt.

> #### info:: Hinweis
> Der oben erwähnte Befehl installiert immer die neuste stabile Version.
> Um eine andere Version zu installieren, kann diese im Befehl wie folgt eingegeben
> werden: `composer create-project contao/standard-edition:4.1.3 <ziel>`

<!-- Quote break -->

> #### info:: Hinweis
> Unter Windows müssen Sie diesen Befehl je nach Konfiguration
> (z.B. Standard XAMPP) möglicherweise als Administrator ausführen.

Während der Installation von Contao werden folgende Parameter der neuen
Installation abgefragt:

```
Some parameters are missing. Please provide them.
database_host (localhost):
database_port (3306):
database_user (null):
database_password (null):
database_name (null):
mailer_transport (mail):
mailer_host (127.0.0.1):
mailer_user (null):
mailer_password (null):
mailer_port (25):
mailer_encryption (null):
prepend_locale (false):
```

Standard-Werte werden in Klammern ausgegeben. Diese Konfiguration wird in der
Datei `app/config/parameters.yml` gespeichert.

> #### info:: Hinweis 
> In Version 4.2 und neuer wird der `secret`-Parameter automatisch
> während der Installation generiert. 
> Weitere Informationen zu dieser Konfiguration ist auf der
> [offiziellen Symfony-Webseite][6] zu finden.


### Wurzelverzeichnis der Webseite

Für den Live-Betrieb muss das Wurzelverzeichnis (Document Root) der Installation
auf den Ordner `web/` gesetzt sein (z.B. über das Admin-Panel des Hosting-Providers).

> #### info:: Hinweis
> Ausführlichere Informationen zur Ordnerstruktur finden sich im [Cookbook][7]
> (auf Englisch).


### Das Contao-Installtool

Um das Contao-Installtool aufzurufen, hängen Sie einfach `/contao/install`
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
Empfehlungen aufmerksam, denn Contao kennt nur seine eigenen Tabellen (die
beginnen mit `tl_`) und wird versuchen, vermeintlich nicht benötigte Tabellen
anderer Programme "aufzuräumen". Bestätigen Sie die Änderungen durch Anklicken
der "Datenbank aktualisieren"-Schaltfläche.


#### Ein Template importieren

Ein Template ist eine vorkonfigurierte Webseite, die eine beispielhafte
Seitenstruktur und verschiedene Stylesheets zur Formatierung der Contao
Core-Module und -Inhaltselemente enthält.

Um ein Template zu importieren, wählen Sie den Eintrag aus dem Drop-Down-Menü
und klicken Sie auf die "Template importieren"-Schaltfläche.

> #### danger:: Achtung
> Beim Import eines Templates werden bestehende Daten überschrieben!


#### Administrator-Konto erstellen

Wenn Sie kein Template importiert haben, müssen Sie ein Administrator-Konto
erstellen, damit Sie sich am Contao-Backend anmelden können. Danach ist der
Installationsprozess abgeschlossen. Der Link unten rechts leitet Sie zur
Backend-Anmeldung weiter.


[1]: https://contao.org/de/download.html
[2]: http://www.winscp.net
[3]: https://github.com/contao/standard-edition
[4]: https://getcomposer.org/download/
[5]: https://getcomposer.org/doc/00-intro.md#using-the-installer
[6]: http://symfony.com/doc/current/reference/configuration/framework.html#secret
[7]: https://docs.contao.org/books/cookbook/en/folder-structure.html