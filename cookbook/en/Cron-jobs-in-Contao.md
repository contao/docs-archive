# Cron jobs in Contao (Poor-Man-Cron)

The `cron.php` file in `system/cron` folder of every Contao installation is
triggered every time a front end page is accessed. Respectively, these cron jobs
only work if your website has visitors. Extensions can use hooks to register
for periodical tasks:

```{.php}
$GLOBALS['TL_CRON']['monthly']
$GLOBALS['TL_CRON']['weekly']
$GLOBALS['TL_CRON']['daily']
$GLOBALS['TL_CRON']['hourly']
$GLOBALS['TL_CRON']['minutely']
```


## Execute cron jobs on the server

To improve reliability of cron jobs, it is better to schedule them on the server
if possible. Otherwise the jobs would not be executed if there are no visitors.
If your server provides such features, you can add the `cron.php` to your 
crontab (or similar) configuration.

Depending on the extensions in your installation, the `cron.php` has to be
executed every minute or else every hour. If you need it to run every
minute, the following configuration is sufficient:

```
* * * * * wget --quiet http://example.com/system/cron/cron.php
```

Be aware that Cronjobs are not executed in parallel, the script will
decide itself what job to run next. A useful configuration if there are no
minutely jobs could look like this:

```
# 22 minutes after every full hour (for hourly jobs)
22 * * * * wget --quiet http://example.com/system/cron/cron.php

# 16 minutes after midnight (for daily jobs)
16 0 * * * wget --quiet http://example.com/system/cron/cron.php

# 10 minutes after midnight every monday (for weekly jobs)
10 0 * * 1 wget --quiet http://example.com/system/cron/cron.php

# 4 minutes after midnight on the 1st each month (for monthly jobs)
4 0 1 * *  wget --quiet http://example.com/system/cron/cron.php
```

*Also make sure your server supports [wget][1] and if the path is correct!*


### Why not execute the PHP file directly?

Instead of using [wget][1], we could also consider executing the PHP script
directly on the server (via CLI). However, this can have serious drawbacks
depending on your Contao configuration. For example if your root page does
not have a domain configured, newsletter emails will be send without absolute
links and will therefore be unusable.


## Workflow of a cron job

In your `fe_page.html5` or `fe_page.xhtml` template, a tiny bit of javascript
is included which retrieves a text file (either using jQuery or MooTools)
that contains the timestamp of the last execution.

```{.js}
// (shortened) MooTools version
new Request({
  url:"system/cron/cron.txt",
  onComplete: function(e) {
    e||(e=0),
    parseInt(e)<Math.round(+(new Date)/1e3)-<?php echo $this->cronTimeout; ?>
    && (new Request({url:"system/cron/cron.php"})).get()
  }
})).get()
```

Depending on the registered jobs (see [`Frontend::getCronTimeout`][3]) a
second ajax request to the `cron.php` is triggered. Using the `tl_cron` table
it verifies again that there are jobs to run and executes the jobs
of the next upcoming interval.

```{.php}
$arrCurrent = array
(
    'monthly'  => date('Ym'),
    'weekly'   => date('YW'),
    'daily'    => date('Ymd'),
    'hourly'   => date('YmdH'),
    'minutely' => date('YmdHi')
);
```

For every call to the `cron.php`, only one of the four available intervals is
executed.

### Please be aware

- The `cron.php` will only be included every minute if there are
  minutely cron jobs registered.
- The order of execution is maintained. `weekly` jobs are only run if the
  `monthly` jobs of the current month have already been executed.


## Testing cron jobs

To manually execute cron jobs for testing purposes, you need to reset multiple
environment settings:

- Delete the `cron.txt` in `system/cron/`
- Delete the entries in the `tl_cron` database table

Now you can open the `cron.php` in a regular browser window to execute the 
next jobs (the order will be maintained!). A successful execution will be
reported to the Contao log in the backend.


[1]: http://en.wikipedia.org/wiki/Wget
[2]: https://github.com/contao/core/blob/3.0.0/assets/contao/js/scheduler-uncompressed.js
[3]: https://github.com/contao/core/blob/3.0.0/system/modules/core/classes/Frontend.php#L601
