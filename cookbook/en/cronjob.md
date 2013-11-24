# Pseudo-Cronjobs in Contao

Each contao installation contains a `cron.php`in the root folder. It is called 
with each frontend page load through the `fe_page.html5`or `fe_page.xhtml` 
template:

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

Many modules hook themself through the following hooks into the pseudo cronjobs:

```
$GLOBALS['TL_CRON']['monthly']
$GLOBALS['TL_CRON']['weekly']
$GLOBALS['TL_CRON']['daily']
$GLOBALS['TL_CRON']['hourly']
```

The smallest interval is hourly.

## Unexpected behaviour

- The cronjob can only be called every 5 minutes
- The script runs from monthly to hourly. When it hits one in the chain it 
will exits the process and the other intervals **won't be processed**.

## Reset cronjob to test

To be able to trigger a cronjob directly you have to reset 3 things:

- Delete the `cron.txt` in `system/html/cron.txt`
- Remove the entries in `localconfig.php`
	- `$GLOBALS['TL_CONFIG']['cron_monthly']`
	- `$GLOBALS['TL_CONFIG']['cron_weekly']`
	- `$GLOBALS['TL_CONFIG']['cron_daily']`
	- `$GLOBALS['TL_CONFIG']['cron_hourly']`
- Reset the entries in the `tl_cron` table