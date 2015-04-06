# Cronjobs in Contao (Poor-Man-Cron)

Die `cron.php` im Verzeichnis `system/cron` jeder Contao-Installation wird beim
Aufruf einer Frontend-Seite ausgeführt. Entsprechend funktionieren diese Cronjobs
standardmäßig nur, wenn die Webseite auch besucht wird. Erweiterungen können
über folgende [Hooks][1] periodische Aufgaben ausführen:

```php
$GLOBALS['TL_CRON']['monthly']
$GLOBALS['TL_CRON']['weekly']
$GLOBALS['TL_CRON']['daily']
$GLOBALS['TL_CRON']['hourly']
$GLOBALS['TL_CRON']['minutely']
```


## Cronjobs auf dem Server ausführen

Um die Zuverlässigkeit der Cronjobs zu verbessern, sollten diese, wenn immer
möglich, direkt über den Server ausgeführt werden. Jobs werden sonst nur
ausgeführt, wenn die Webseite auch besucht wird. Sollte Ihr Server entsprechende
Möglichkeiten bieten, können Sie die `cron.php` in der Crontab (oder
entsprechender Konfiguration) einrichten.

Abhängig von den vorhandenen Erweiterungen in Ihrem System muss die `cron.php`
jede Minute oder aber nur jede Stunde ausgeführt werden. Für jede Minute reicht
folgende Konfiguration, das Script entscheidet dann selber was zu tun ist.

```
* * * * * wget -O /dev/null -q http://example.com/system/cron/cron.php
```

Zu beachten ist dabei auch, dass die Cronjobs nicht gleichzeitig arbeiten,
und das Script selber entscheidet welche Jobs als nächstes bearbeitet werden.
Eine sinnvolle Konfiguration, falls keine minütlichen Aufgaben anstehen, könnte
folgendermaßen aussehen:

```
# 22 Minuten nach jeder vollen Stunde (für hourly-Jobs)
22 * * * * wget -O /dev/null -q http://example.com/system/cron/cron.php

# 16 Minuten nach Mitternacht (für daily-Jobs)
16 0 * * * wget -O /dev/null -q http://example.com/system/cron/cron.php

# 10 Minuten nach Mitternacht jeden Montag (für weekly-Jobs)
10 0 * * 1 wget -O /dev/null -q http://example.com/system/cron/cron.php

# 4 Minuten nach Mitternacht am 1. jedes Monats (für monthly-Jobs)
4 0 1 * *  wget -O /dev/null -q http://example.com/system/cron/cron.php
```

*Prüfen Sie außerdem, dass auf Ihrem Server [wget][2] verfügbar ist und der
Pfad stimmt!*


### Die PHP-Datei direkt ausführen?

Anstatt den "Umweg" über [wget][2] zu machen, könnte die PHP ja auch direkt
(via CLI) aufgerufen werden. Dies hat aber je nach Konfiguration Nachteile.
Sollte beispielsweise in der Root-Seite keine Domain eingetragen sein, werden
beim Versand von Newslettern keine absoluten URLs generiert und die E-Mail ist
entsprechend unbrauchbar.


## Funktionsweise des Cron-Aufrufs

Im `fe_page.html5` bzw. `fe_page.xhtml` Template wird ein kleines Stück 
Javascript eingebunden, welches (entweder per jQuery oder MooTools) eine
Textdatei abfragt, die den Zeitstempel der letzten Ausführung enthält.

```js
// (gekürzte) MooTools-Variante
new Request({
  url:"system/cron/cron.txt",
  onComplete: function(e) {
    e||(e=0),
    parseInt(e)<Math.round(+(new Date)/1e3)-<?php echo $this->cronTimeout; ?>
    && (new Request({url:"system/cron/cron.php"})).get()
  }
})).get()
```

Abhängig von den vorhandenen Jobs (siehe [`Frontend::getCronTimeout`][4]) wird
falls nötig ein zweiter Ajax-Request auf die `cron.php` ausgeführt. 
Diese prüft zuerst nochmals anhand der Tabelle `tl_cron`, ob Jobs ausgeführt
werden sollen und welches der vier Ausführungsintervalle als nächstes an
der Reihe ist. 

```php
$arrCurrent = array
(
    'monthly'  => date('Ym'),
    'weekly'   => date('YW'),
    'daily'    => date('Ymd'),
    'hourly'   => date('YmdH'),
    'minutely' => date('YmdHi')
);
```

Pro Aufruf der `cron.php` wird maximal eines der vier Intervalle ausgeführt.


### Zu beachten gilt

- Die `cron.php` wird nur jede Minute aufgerufen, wenn auch
  Jobs für `minutely` vorhanden sind.
- Die Reihenfolge wird berücksichtigt. `weekly`-Jobs werden erst ausgeführt,
  wenn die `monthly`-Jobs des aktuellen Monats erledigt sind.


## Cronjob testen

Um Cronjobs zu Testzwecken manuell auszuführen, müssen folgende
Umgebungsvariablen zurückgesetzt werden:

- Die `cron.txt` unter `system/cron/` löschen
- Die Einträge in der Tabelle `tl_cron` löschen

Danach kann die `cron.php` normal im Browser aufgerufen werden, um die
nächsten Jobs (beachten Sie die Reihenfolge!) auszuführen. Eine erfolgreiche
Ausführung ist im Backend unter System-Log sichtbar.

[1]: Hooks-in-Contao.md
[2]: http://de.wikipedia.org/wiki/Wget
[3]: https://github.com/contao/core/blob/3.0.0/assets/contao/js/scheduler-uncompressed.js
[4]: https://github.com/contao/core/blob/3.0.0/system/modules/core/classes/Frontend.php#L601
