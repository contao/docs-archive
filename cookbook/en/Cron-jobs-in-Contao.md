# Cron jobs in Contao (Poor-Man-Cron)

The `cron.php` file in the root folder of every Contao installation is triggered
every time a front end page is accessed. Respectively, these cron jobs only work
if your website has visitors. Extensions can use hooks to register for periodical
tasks:

```php
$GLOBALS['TL_CRON']['monthly']
$GLOBALS['TL_CRON']['weekly']
$GLOBALS['TL_CRON']['daily']
$GLOBALS['TL_CRON']['hourly']
```

The smallest possible interval for Contao 2.11 is hourly execution.


## Execute cron jobs on the server

To improve reliability of cron jobs, it is better to schedule them on the server
if possible. Otherwise the jobs would not be executed if there are no visitors.
If your server provides such features, you can add the `cron.php` to your 
crontab (or similar) configuration.

Do not execute the file more than every five minutes. Be aware that Cronjobs
are not executed in parallel, the script will decide itself what job to
run next. A useful configuration could look like this:

```
# 22 minutes after every full hour (for hourly jobs)
22 * * * * wget -O /dev/null -q http://example.com/cron.php

# 16 minutes after midnight (for daily jobs)
16 0 * * * wget -O /dev/null -q http://example.com/cron.php

# 10 minutes after midnight every monday (for weekly jobs)
10 0 * * 1 wget -O /dev/null -q http://example.com/cron.php

# 4 minutes after midnight on the 1st each month (for monthly jobs)
4 0 1 * *  wget -O /dev/null -q http://example.com/cron.php
```

By using a delay of six minutes, two jobs can never be executed at the same time.
*Also make sure your server supports [wget][1] and if the path is correct!*


### Why not execute the PHP file directly?

Instead of using [wget][1], we could also consider executing the PHP script
directly on the server (via CLI). However, this can have serious drawbacks
depending on your Contao configuration. For example if your root page does
not have a domain configured, newsletter emails will be send without absolute
links and will therefore be unusable.


## Workflow of a cron job

Your `fe_page.html5` or `fe_page.xhtml` template contains the following 
javascript code which is responsible for executing the `cron.php`. First of all,
a text file is retrieved that contains the timestamp of the last execution.

```js
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

Only every five minutes a second ajax request to the `cron.php` is triggered.
Using the `tl_lock` table, it verifies again that at least five minutes have
passed since the last execution. If that's the case, it will trigger the jobs
of the next upcoming interval. This information is stored in the `localconfig.php`.

```php
$GLOBALS['TL_CONFIG']['cron_monthly']
$GLOBALS['TL_CONFIG']['cron_weekly']
$GLOBALS['TL_CONFIG']['cron_daily']
$GLOBALS['TL_CONFIG']['cron_hourly']
```

For every call to the `cron.php`, only one of the four available intervals is
executed. After a successful run, the `localconfig.php` is updated and the
process is terminated.

### Please be aware

- Cron jobs will only be executed every five minutes.
- The order of execution is maintained. `weekly` jobs are only run if the
  `monthly` jobs of the current month have already been executed.
- If a job terminates the process (e.g. due to an exception), all following
  jobs are not executed and the last execution date will not be updated!


## Testing cron jobs

To manually execute cron jobs for testing purposes, you need to reset multiple
environment settings:

- Delete the `cron.txt` in `system/html/`
- Delete the respective last execution timestamp in your `localconfig.php`
- Delete the entry in the `tl_lock` database table

Now you can open the `cron.php` in a regular browser window to execute the 
next jobs (the order will be maintained!). A successful execution will be
reported to the Contao log in the backend.


[1]: http://en.wikipedia.org/wiki/Wget
