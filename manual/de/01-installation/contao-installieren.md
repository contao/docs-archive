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

> **Warning** Die URL zeigt aktuell auf die neuste Contao 3.x.x Version.
Um Contao 4 zu installieren, fügen sie die Version zur URL hinzu, z.B. "/4.0.2".
Beispiel: curl -L http://download.contao.org/4.0.2 | tar -xzp


### Installation mit Composer

Mit Composer kann Contao über die [contao/standard-edition][6] installiert
werden.

```bash
php composer.phar create-project contao/standard-edition <ziel>
```

Geben Sie als `<ziel>` den Ordner ein, in welchen die Contao-Dateien
installiert werden sollen. Wenn der Ordner nicht vorhanden ist, wird er
automatisch angelegt.

> **Info** Der oben erwähnte Befehl installiert immer die neuste stabile Version.
Um eine andere Version zu installieren, kann diese im Befehl wie folgt eingegeben
werden: `php composer.phar create-project contao/standard-edition:4.0.2 <ziel>`

Bevor Sie diesen Befehl ausführen können, muss [Composer installiert sein][7].
Mit folgendem Befehl kann Composer global auf einem Mac OS X oder Linux-System
installiert werden:

```bash
curl -sS https://getcomposer.org/installer | php
sudo mv composer.phar /usr/local/bin/composer
```

Unter Windows erfolgt die Installation mittels dem [Installer][10].

Während der Installation von Contao werden folgende Parameter der neuen
Installation abgefragt:

```bash
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
secret (ThisTokenIsNotSoSecretChangeIt):
```

Standard-Werte werden in Klammern ausgegeben. Diese Konfiguration wird in der
Datei `app/config/parameters.yml` gespeichert.

Der `secret`-Parameter wird für Verschlüsselungen und gegen [CSRF][8]-Attacken
verwendet. Es ist wichtig hier einen sicheren Schlüssel einzugeben.
Die Symfony-Dokumentation sagt dazu:

> **Note** Der Wert sollte aus zufälligen Buchstaben, Zahlen und
Symbolen bestehen. Die empfohlene Länge liegt bei 32 Zeichen.

Weitere Informationen zu dieser Konfiguration ist auf der
[offiziellen Symfony-Webseite][9] zu finden.


### Das Contao-Installtool

Um das Contao-Installtool aufzurufen, hängen Sie einfach `install.php`
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

> **Danger** Beim Import eines Templates werden bestehende Daten überschrieben!


#### Administrator-Konto erstellen

Wenn Sie kein Template importiert haben, müssen Sie ein Administrator-Konto
erstellen, damit Sie sich am Contao-Backend anmelden können. Danach ist der
Installationsprozess abgeschlossen. Der Link unten rechts leitet Sie zur
Backend-Anmeldung weiter.


[1]: https://contao.org/de/download.html
[2]: http://www.winscp.net
[6]: https://github.com/contao/standard-edition
[7]: https://getcomposer.org/download/
[8]: https://de.wikipedia.org/wiki/Cross-Site-Request-Forgery
[9]: http://symfony.com/doc/current/reference/configuration/framework.html#secret
[10]: https://getcomposer.org/doc/00-intro.md#using-the-installer
