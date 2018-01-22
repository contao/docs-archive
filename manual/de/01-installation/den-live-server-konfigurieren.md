## Den Live-Server konfigurieren

In diesem Kapitel geht es nicht darum, den Apache-Dienst zu installieren oder
PHP zu kompilieren, was auf einem Shared-Hosting-Server ohnehin nicht möglich
ist. Stattdessen wird erklärt, wie man die Contao-Systemvoraussetzungen prüft
und PHP 5 aktiviert.


### Contao-Systemvoraussetzungen

#### Systemvoraussetzungen Kernsystem (manuelle Installation)

Contao benötigt einen Webserver wie Apache oder IIS mit PHP- und MySQL-Support
sowie verschiedene PHP-Erweiterungen.

|Contao-Version       | 3.5 LTS                 | 4.4 LTS                      | 4.5         |
|---------------------|-------------------------|------------------------------|-------------|
| PHP ab Version:     | 5.4.0                   | 5.6.0                        | 7.1       |     
| MySQL ab Version:   | 5.0.3                   | 5.0.3                        | 5.5.7    |
| PHP-Erweiterungen:  | GDlib (Bildbearbeitung) | GD, Imagick oder Gmagick     | GD, Imagick oder Gmagick|
|                     | DOM (XML-Dateien)       | DOM (XML-Dateien)            | DOM (XML-Dateien)|
|                     |\-                       | intl (Internationalisierung) | intl (Internationalisierung)|
|                     |                         | Umleitung auf app.php        | Umleitung auf app.php|
| Rechte PHP-Prozess: |\-                       | Symlinks anlegen und folgen  | Symlinks anlegen und folgen|
|                     |\-                       | Dateien anlegen und ändern   | Dateien anlegen und ändern|
| DocumentRoot        |\-                       | Auf Ordner "web" setzen      | Auf Ordner "web" setzen|

> #### info:: Hinweis
> Je nach installierten Extensions kann es außerdem notwendig sein die PHP 
> Variable `max_input_vars` zu erhöhen (bspw. auf `2000` oder höher). Andernfalls 
> können zu lange Backend Formulare nicht komplett abgeschickt werden.

Contao wurde erfolgreich in allen modernen Browsern wie Firefox oder Internet
Explorer (ab Version 9) getestet.

#### Systemvoraussetzungen Composer-Paketverwaltung: Kommandozeile und Contao-Manager

Zusätzlich zu den Systemvoraussetzungen des Kernsystems:

- ausreichend Arbeitsspeicher (RAM) für Konsolenbefehle, ggf. mehrere GB
- lange Skriptlaufzeit für Konsolenbefehle
- PHP Phar-Erweiterung
- PHP cURL-Erweiterung
- PHP OpenSSL-Erweiterung
- PHP-Flag "allow_url_fopen" aktiv
- PHP-Funktionen "proc_open" und "proc_close"
- Für Kommandozeilenzugriff: SSH-Zugang



### Der Contao-Check

Laden Sie den Contao-Check herunter und finden Sie heraus, ob Ihr Server die
Contao-Systemvoraussetzungen erfüllt.

![](images/contao-check.jpg)

Entpacken Sie die Zip-Datei, übertragen Sie den Ordner
`check` in Ihr Contao-Verzeichnis und öffnen Sie ihn in einem Browser.

[Den Contao-Check herunterladen][1] | [Zum Projekt auf GitHub][2]

> #### info:: Hinweis
> Eine Contao 4 Installation kann mit dem Contao Check nicht validiert werden.


### Provider-spezifische Einstellungen

Es gibt ein paar wenige große Internet Service Provider, die spezielle
Einstellungen für den Betrieb von Contao erfordern. Zum Glück sind sie nur die
Ausnahme von der Regel. Die Provider-spezifische Einstellungen finden Sie im
[Contao-Forum][3]. Sorgenfreies Contao-Hosting erhalten Sie bei den
[Contao Hosting-Partnern][4].


[1]: https://github.com/contao/check/zipball/master
[2]: https://github.com/contao/check
[3]: https://community.contao.org/de/forumdisplay.php?67-Erfahrungen-mit-Webhostern
[4]: https://contao.org/de/partners.html?search=services&for=partner_hosting
