## Manual update

When it comes to manually updating a Contao installation, you can either upload
the whole Contao download archive to the server (replacing files) or you can
upload only the files that have been modified since the last update
(synchronizing files). Either way, you should always back up the following files
and folders - just in case there is an error or you accidentally override them:

* `files/*`
* `system/config/dcaconfig.php`
* `system/config/initconfig.php`
* `system/config/langconfig.php`
* `system/config/localconfig.php`
* `templates/*`

This will back up your local configuration, your custom templates and your
files.


### Replacing files

Replacing the files of a Contao installation is pretty simple. Just unpack the
Contao download archive on the server or extract it on your local computer and
upload the files with an FTP client. Then restore the files that you have backed
up and remove potential leftovers from earlier Contao versions.

**Attention:** If you have installed any third-party extensions, make sure to
backup and restore them, too, or do not overwrite them at all. Otherwise you
will have to reinstall the modules and depending on the extension you might
eventually lose data!


### Synchronizing files

To synchronize a Contao installation, you can either use the [Unix diff
utility][1] or an FTP program. Unix utilities are typically used by server
administrators only, so they will not be explained here. To synchronize files
via FTP, open WinSCP and connect to the server. Backup the files mentioned above
and then navigate to the Contao directory and click the "Synchronize files"
button.

![](images/synchronization-options.jpg)

Review the options carefully and make sure to choose "Preview changes", so you
can check which files will be updated. Then confirm each file in the preview
window and double check the files that are marked for deletion! Click "OK" to
start the synchronization process.

![](images/synchronization-confirmation.jpg)


### Updating the database

After you have updated the Contao files, you need to update the database, too.
Fortunately, the Contao install tool will do most of the work for you. Just open
it and enter your password, then scroll down to the database section and confirm
the changes.


### Purge the internal cache

Finally you should also rebuild the internal cache (for DCA and language files). 
In the backend go to "Maintenance" and check "Purge the internal cache" in 
the "Purge data" section. Confirm the action by clicking on "Purge data".

You will now receive a message in the header asking to rebuild the internal 
cache. Click on "Build the cache" to cache the internal files.


[1]: http://en.wikipedia.org/wiki/Diff
