## Installing Contao

First of all, download the [latest Contao archive][1] and extract it on your
local computer. Move the files into the `htdocs` folder of your local
installation (e.g. XAMPP) or upload them to your server with an FTP program (we
recommend using [WinSCP][2]). Depending on your server configuration, the public
folder is most likely called `htdocs`, `httpdocs`, `html` or `public_html`.

If you have SSH access, you can download and extract the archive with the
following commands:

```bash
curl -L http://download.contao.org/4.0.2 | tar -xzp
```


### The Contao install tool

To open the Contao install tool, simply add `/install.php` to the URL of
your Contao installation. Note that the install tool is protected against brute
force attacks and will be locked if a wrong password has been entered three
times in a row. To remove the lock, open file `system/config/localconfig.php` in
a text editor, find the following line and set it to `0`.

```php
$GLOBALS['TL_CONFIG']['installCount'] = 0; // This will remove the automatic lock
```


#### Connecting to the database

Log into your server administration panel (e.g. "Plesk" or "cPanel") and create
a new database for Contao. Then enter the login credentials in the Contao
install tool. Note that the Contao default character set `UTF-8` is written as
`UTF8` in MySQL!


#### Updating the database tables

Once you are connected to the database, Contao automatically checks its tables
and displays a list of recommended changes in case they are not up to date. Make
sure to read those recommendations carefully, because Contao only knows its own
tables (prefixed with `tl_`) and will try to remove those of other applications
eventually sharing the database. Confirm the changes and click the "Update
database" button.


#### Importing a template

A template is a predetermined website with an exemplary page structure and different
style-sheets to format the Contao core modules and content elements.

To import a template, select the entry from the drop-down menu and click the "Import
template" button.

**When importing a template, existing data will be replaced!**


#### Creating an admin user

If you did not import a template, you have to create an admin user to log into
the Contao back end. After you have created the account, the installation
process is completed. The link in the lower right corner will take you to the
administration area.


[1]: https://contao.org/en/download.html
[2]: http://www.winscp.net/
