> TODO: rewrite

# Cron job vs. periodic command scheduler

Contao by default has a *periodic command scheduler* activated (see: ``System`` / ``Settings`` / ``Front end
configuration`` in the backend) to trigger different reappearing tasks that - right now - can be registered by adding 
classes and function names to one of the following global arrays:  
   
```php
$GLOBALS['TL_CRON']['minutely']
$GLOBALS['TL_CRON']['hourly']
$GLOBALS['TL_CRON']['daily']
$GLOBALS['TL_CRON']['weekly']
$GLOBALS['TL_CRON']['monthly']
```

As there is no continuous process running, the only way to possibly execute these tasks is whenever a user visits the
site. This has two big drawbacks:
* It can in now way be guaranteed that a certain task will run (no visitor means no trigger).
* Frontend performance might suffer under a heavy / time consuming task.

**What's the alternative?**

So for a production environment the periodic command scheduler should be disabled and a *real* cron job set up. This
basically means that your operating system needs to trigger a special route of your page in regular intervals.     

## Setup a cron job
To make Contao's tasks run the ``_contao/cron`` route must be triggered (so for example
``http://yourdomain.com/_contao/cron``). To be able to use minutely scheduled tasks you should at least trigger it once
a minute.
 
### Linux / Mac
On linux you can simply add a new cron job by editing the cron table (``crontab -e``) and adding a new line. See the
following example to trigger the route every minute for ``http://yourdomain.com`` (while ignoring the output):

    * * * * * wget -O -http://yourdomain.com/_contao/cron > /dev/null 2>&1

In most cases the use of ``wget`` is a better choice than trying to call the php executable directly on the command line
as the console's execution environment often differs from the one of the web process.            

### Windows
One windows alternative to cron jobs is called ``Schtasks`` and is available in newer windows versions (>= Windows 8). 
See the [documentation](https://technet.microsoft.com/en-us/library/cc725744.aspx). You might also have a look at these
[other alternatives](https://stackoverflow.com/questions/132971/what-is-the-windows-version-of-cron).