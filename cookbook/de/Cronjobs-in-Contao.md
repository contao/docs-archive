# Cronjobs in Contao (Poor-Man-Cron)

Die `cron.php` im Root-Ordner jeder Contao-Installation wird beim Aufruf einer
Frontend-Seite ausgeführt. Entsprechend funktionieren diese Cronjobs
standardmässig nur, wenn die Webseite auch besucht wird. Erweiterungen können
über folgende [Hooks][1] periodische Aufgaben ausführen:

```
$GLOBALS['TL_CRON']['monthly']
$GLOBALS['TL_CRON']['weekly']
$GLOBALS['TL_CRON']['daily']
$GLOBALS['TL_CRON']['hourly']
```

Der kleinstmögliche Interval bei Contao 2.11 ist stündlich.


## Cronjobs auf dem Server ausführen

Um die Zuverlässigkeit der Cronjobs zu verbessern, sollten diese wenn immer
möglich direkt über den Server ausgeführt werden. Jobs werden sonst nur
ausgeführt wenn die Webseite auch besucht wird. Sollte Ihr Server entsprechende
Möglichkeiten bieten, können Sie die `cron.php` in der Crontab (oder
entsprechender Konfiguration) einrichten.

Führen Sie die Datei maximal alle fünf Minuten aus. Zu beachten ist dabei auch,
dass die Cronjobs nicht gleichzeitig arbeiten, und das Script selber entscheidet
welche Jobs als nächstes bearbeitet werden. Eine sinnvolle Konfiguration könnte
folgendermassen aussehen:

```
# 22 Minuten nach jeder vollen Stunde (für hourly-Jobs)
22 * * * * wget --silent http://example.com/cron.php

# 16 Minuten nach zwölf (für daily-Jobs)
16 0 * * * wget --silent http://example.com/cron.php

# 10 Minuten nach zwölf jeden Montag (für weekly-Jobs)
10 0 * * 1 wget --silent http://example.com/cron.php

# 4 Minuten nach zwölf am 1. jedes Monats (für monthly-Jobs)
4 0 1 * *  wget --silent http://example.com/cron.php
```

Durch den Abstand von sechs Minuten wird eine Überschneidung verhindert.
*Prüfen Sie ausserdem dass auf Ihrem Server [wget][2] verfügbar ist und der
Pfad stimmt!*


### Die PHP-Datei direkt ausführen?

Anstatt den "Umweg" über [wget][2] zu machen, könnte die PHP ja auch direkt
(via CLI) aufgerufen werden. Dies hat aber je nach Konfiguration Nachteile.
Sollte beispielsweise in der Root-Seite keine Domain eingetragen sein, werden
beim Versand von Newslettern keine absoluten URLs generiert und die Email ist
entsprechend unbrauchbar.


## Funktionsweise des Cron-Aufrufs

Im `fe_page.html5` bzw. `fe_page.xhtml` Template ist folgender Javascript-Code
zuständig für den Aufruf der `cron.php`. Dabei wird zuerst eine Textdatei
abgefragt, welche den Zeitstempel der letzten Ausführung enthält.

```{.js}
new Request({
  url:'system/html/cron.txt',
  onComplete: function(txt) {
    if (!txt) txt = 0;
    if (parseInt(txt) < (Math.round(+new Date()/1000) - 300)) {
      new Request({url:'cron.php'}).get();
    }
  }
}).get();
```

Nur alle fünf Minuten wird ein zweiter Ajax-Request auf die `cron.php`
ausgeführt. Diese prüft zuerst nochmals anhand der Tabelle `tl_lock`,
ob in den letzten fünf Minuten keine Cronjobs ausgeführt wurden.
Danach wird geprüft, welcher der vier Ausführungsintervallen als nächstes
an der Reihe ist. Die entsprechenden Informationen stehen in der
`localconfig.php`.

```{.php}
$GLOBALS['TL_CONFIG']['cron_monthly']
$GLOBALS['TL_CONFIG']['cron_weekly']
$GLOBALS['TL_CONFIG']['cron_daily']
$GLOBALS['TL_CONFIG']['cron_hourly']
```

Pro Aufruf der `cron.php` wird maximal einer der vier Intervalle ausgeführt.
Danach wird die `localconfig.php` aktualisiert und der Prozess beendet.


### Zu beachten gilt

- Cronjobs werden nur alle fünf Minuten ausgeführt
- Die Reihenfolge wird berücksichtigt. `weekly`-Jobs werden erst ausgeführt, wenn die `monthly`-Jobs des aktuellen Monats erledigt sind.
- Bricht ein Job den Prozess beispielsweise durch eine Exception ab, werden
alle weitere Jobs nicht ausgeführt, da das letzte Ausführungsdatum nicht
aktualisiert wird!


## Cronjob testen

Um Cronjobs zu Testzwecken manuell auszuführen, müssen mehrere
Umgebungsvariablen zurückgesetzt werden:

- Die `cron.txt` unter `system/html/cron.txt` löschen
- Den entsprechenden Eintrag in der `localconfig.php` löschen
- Den Eintrag in der Tabelle `tl_lock` löschen

Danach kann die `cron.php` normal im Browser aufgerufen werden, um die
nächsten Jobs (beachten Sie die Reihenfolge!) auszuführen. Eine erfolgreiche
Ausführung ist im Backend unter System-Log sichtbar.

[1]: Hooks-in-Contao.md
[2]: http://de.wikipedia.org/wiki/Wget
