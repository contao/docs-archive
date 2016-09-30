## Updating Contao

Contao 4 can be updated through Composer. This includes the core system
(contao/core-bundle) and all its dependencies (Symfony, bundles, external
libraries, etc.).

Before an update, you should always back up the following files and folders
just in case there is an error or you accidentally override them:

* `files/*`
* `system/config/dcaconfig.php`
* `system/config/initconfig.php`
* `system/config/langconfig.php`
* `system/config/localconfig.php`
* `templates/*`

This will back up your local configuration, your custom templates and your
files.


### Updating with SSH and Composer

This method requires to have SSH enabled and Composer installed on your server.
You can find the commands for installing Composer on your server on
[the official Composer website][2].

The values for the directives [memory_limit][3] and [max_execution_time][4]
should be sufficient in order to complete successfully the update. These values
can sometimes be changed according to the web hosting service you have.

> #### info:: Note
> Before updating Contao, you can remove entirely the `vendor/` folder to avoid
> keeping unused dependencies or to avoid having potential problems.

Then, you can updating Contao with the following command:

```bash
php composer.phar update
```


### Updating manually

When it comes to manually updating a Contao installation, you can either upload
the whole Contao download archive to the server (replacing files) or you can
upload only the files that have been modified since the last update
(synchronizing files).

Do not forget to save the folders and files mentioned above before performing
your update.


#### Replacing files

Replacing the files of a Contao installation is pretty simple. Just unpack the
Contao download archive on the server or extract it on your local computer and
upload the files with an FTP client. Then restore the files that you have backed
up and remove potential leftovers from earlier Contao versions.

> #### warning:: Warning
> If you have installed any third-party extensions, make sure to
> backup and restore them, too, or do not overwrite them at all. Otherwise you
> will have to reinstall the modules and depending on the extension you might
> eventually lose data!


#### Synchronizing files

To synchronize a Contao installation, you can either use the [Unix diff
utility][1] or an FTP program. Unix utilities are typically used by server
administrators only, so they will not be explained here. To synchronize files
via FTP, open WinSCP and connect to the server. Backup the files mentioned above
and then navigate to the Contao directory and click the "Synchronize files"
button.

Review the options carefully and make sure to choose "Preview changes", so you
can check which files will be updated. Then confirm each file in the preview
window and double check the files that are marked for deletion! Click "OK" to
start the synchronization process.


#### Updating the database

After you have updated the Contao files, you need to update the database, too.
Fortunately, the Contao install tool will do most of the work for you. Just open
it and enter your password, then scroll down to the database section and confirm
the changes.


### Purge the cache

Finally you should also rebuild the cache. In the back end go to "Maintenance"
and check [...] in the "Purge data" section. Confirm the action by clicking on
"Purge data".


[1]: http://en.wikipedia.org/wiki/Diff
[2]: https://getcomposer.org/download/
[3]: http://php.net/manual/en/ini.core.php#ini.memory-limit
[4]: http://php.net/manual/en/info.configuration.php#ini.max-execution-time
