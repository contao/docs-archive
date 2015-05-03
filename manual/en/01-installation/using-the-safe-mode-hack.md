## Using the Safe Mode Hack

While trying to install Contao with the install tool, you might have seen a
warning that the local configuration file is not writable.

![](images/localconfig-not-writable.jpg)


### File permission issues

The term "Safe Mode Hack" is actually misleading, because it implies that the
problem was caused by the PHP `safe_mode`. However, it is caused by insufficient
file permissions and can occur even if `safe_mode` is disabled, so it should be
called "File Permission Hack" instead. PHP as an Apache module is typically run
as `wwwrun`, `www-data` or `nobody`, whereas the files that you upload via FTP
belong to you (e.g. `web4` or `ab5678`). The server therefore denies the PHP
script Contao access to those files.


#### Using FTP for file operations

To work around the permission problem, Contao establishes an FTP connection to
modify files and folders. All you have to do is to enter your FTP login details.
Take special care when entering the relative path from your FTP root directory
to the Contao folder (e.g. `html/`, `public_html/` or `httpdocs/`).

A few directories still require write permissions, because PHP will access them
directly:

* `assets/images`
* `assets/images/*`
* `system/logs`
* `system/tmp`

The permissions (CHMOD 777) are set by the install tool automatically and do not
have to be adjusted manually normally. Should it be necessary, please **only
adjust the three directories mentioned above** – despite what you might have
read in a tutorial or in the Contao forums!
