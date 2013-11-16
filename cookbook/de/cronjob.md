# Pseudo-Cronjobs in Contao

Jede Contao Installation enthält eine `cron.php` im root Ordner. Diese wird bei jedem Seitenaufruf einer Frontendseite über das `fe_page.html5` oder `fe_page.xhtml` Template getriggert:

```
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

Viele Module hängen sich über folgende Hooks in den Pseudo Cronjob ein:

```
$GLOBALS['TL_CRON']['monthly']
$GLOBALS['TL_CRON']['weekly']
$GLOBALS['TL_CRON']['daily']
$GLOBALS['TL_CRON']['hourly']
```

Die kleinst möglichste Interval ist hier also Stündlich.

## Unerwartete Verhaltensweisen

- Der Cronjob wird nur alle 5min getestet
- Das Script arbeitet sich von Monatlich zu Stündlich durch, wenn einer in der Kette abgearbeitet wird, wird der Prozess danach abgebrochen und die weiteren werden **nicht mehr ausgeführt**.

## Cronjob zum Testen zurücksetzen

Um den Cronjob direkt zu triggern muss man ihn an 3 Punkten zurücksetzen:

- Die `cron.txt` unter `system/html/cron.txt`löschen
- Die Einträge in der `localconfig.php` löschen
	- `$GLOBALS['TL_CONFIG']['cron_monthly']`
	- `$GLOBALS['TL_CONFIG']['cron_weekly']`
	- `$GLOBALS['TL_CONFIG']['cron_daily']`
	- `$GLOBALS['TL_CONFIG']['cron_hourly']`
- Die Einträge in der `tl_cron` Tabelle leeren
