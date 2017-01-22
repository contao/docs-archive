## Contao aktualisieren

Contao 4 kann über den den Composer aktualisiert werden. Das inkludiert das Kern-System (`contao/core-bundle` und sonstige Contao Bundles) und dessen Abhängigkeiten (Synfony, Bundles, externe Bibliotheken, etc.).

Vor einem Update sollten auf jeden Fall folgende Dateien und Ordner gesichert werden, falls etwas schief geht oder diese unabsichtlich überschrieben werden:

* `app/config/parameters.yml`
* `files/*`
* `system/config/dcaconfig.php`
* `system/config/initconfig.php`
* `system/config/langconfig.php`
* `system/config/localconfig.php`
* `templates/*`

Dieses Backup umfasst Ihre lokale Konfiguration, eventuell angepasste Templates
sowie die hochgeladenen Dateien.

### Mit SSH und Composer aktualisieren

Diese Methode setzt die Möglichkeit voraus sich über SSH zu verbinden und dass Composer am Server installiert ist. Wir Composer installiert werden kann findet man auf [der offiziellen Composer Website][3].

Die Werte für die PHP Einstellungen [memory_limit][4] und [max_execution_time][5] sollten ausreichend hoch gesetzt sein, damit eine Aktualisierung erfolgreich durchgeführt werden kann. Normalerweise sind diese Werte in einer Kommandozeilen-Umgebung von PHP unlimitiert, das kann sich aber von Hoster zu Hoster unterscheiden. In so einem Fall sollte man direkt den Support des Hosters kontaktieren.

Contao kann danach z.B. mit dem folgenden Kommando aktualisiert werden
```bash
composer update
```

### Manuelles update

Bei einem manuellen Update einer Contao Installation könnte man entweder das komplette Download Archiv der neuen Contao Version auf den Server kopieren (Dateien ersetzen) oder man kopiert nur die Dateien, die sich seit dem letzten Update geändert haben (Dateien synchronisieren).

Hier ist es besonders wichtig nicht zu vergessen die Eingangs erwähnten Dateien und Ordner vorher zu sichern.

#### Dateien ersetzen

Die Dateien einer Contao-Installation zu ersetzen ist relativ simpel. Übertragen
Sie einfach das Contao-Archiv auf Ihren Server oder entpacken Sie es auf Ihrem
lokalen Rechner und kopieren Sie die Dateien anschließend mit einem FTP-Programm
(wir empfehlen [WinSCP][1]). Danach stellen Sie die Dateien aus dem Backup
wieder her und entfernen eventuelle Überbleibsel vorheriger Contao-Versionen.

> #### warning:: Vorsicht
> Wenn Sie Third-Party-Erweiterungen installiert haben, müssen Sie
> diese ebenfalls sichern und nach dem Update wiederherstellen oder darauf achten,
> sie gar nicht erst zu überschreiben. Andernfalls müssen diese Module neu
> installiert werden, was bei einigen Erweiterungen zu Datenverlust führen kann!


#### Dateien synchronisieren

Um eine Contao-Installation zu synchronisieren, können Sie entweder das [Unix
Diff-Programm][2] oder einen FTP-Client verwenden. Unix-Utilities werden
normalerweise nur von Serveradministratoren verwendet, daher werden sie hier
nicht erklärt. Um Dateien per FTP zu synchronisieren, öffnen Sie WinSCP und
verbinden Sie sich mit dem Server. Erstellen Sie ein Backup der oben genannten
Dateien und navigieren Sie dann zum Contao-Verzeichnis und klicken Sie auf die
"Dateien synchronisieren"-Schaltfläche.

Treffen Sie Ihre Auswahl wie in der Abbildung und wählen Sie unbedingt die
Option "Änderungsvorschau" aus, damit Sie die zu aktualisierenden Dateien noch
einmal prüfen können. Bestätigen Sie danach die Einstellungen im Vorschaufenster
und achten Sie besonders auf die zu löschenden Ressourcen! Klicken Sie "OK", um
den Synchronisationsvorgang zu starten.


#### Die Datenbank aktualisieren

Nachdem Sie die Contao-Dateien aktualisiert haben, müssen Sie noch die Datenbank
auf den neuesten Stand bringen. Diese Arbeit übernimmt das Contao-Installtool
für Sie. Geben Sie Ihr Passwort ein, scrollen Sie bis zum Datenbank-Abschnitt
und bestätigen Sie die Änderungen.


### Den Cache leeren

Zum Schluss muss noch der Symfony Cache mit dem Kommando `php bin/console cache:clear -e=prod` über die Kommandozeile gelöscht werden.

[1]: http://www.winscp.net
[2]: http://de.wikipedia.org/wiki/Diff
[3]: https://getcomposer.org/download/
[4]: http://php.net/manual/en/ini.core.php#ini.memory-limit
[5]: http://php.net/manual/en/info.configuration.php#ini.max-execution-time
