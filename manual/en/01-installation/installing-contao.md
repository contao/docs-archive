## Installing Contao

First of all, download the [latest Contao archive][1] and extract it on your
local computer. Move the files into the `htdocs` folder of your local
installation (e.g. XAMPP) or upload them to your server with an FTP program (we
recommend using [WinSCP][2]). Depending on your server configuration, the public
folder is most likely called `htdocs`, `httpdocs`, `html` or `public_html`.

If you have SSH access, you can download and extract the archive with the
following commands:

```bash
curl -L http://download.contao.org | tar -xzp
```


### The Contao install tool

To open the Contao install tool, simply add `/contao/install.php` to the URL of
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
tables and will try to remove those of other applications eventually sharing the
database. Confirm the changes and click the "Update database" button.


#### Importing a template

A template is a predetermined website with an exemplary
page structure and different style-sheets to format the Contao
core modules and content elements.

Since version 3.2.11, the sample web-page is no longer included in the download package.
Depending on the version used, the new [*Contao Official Demo*][3] 
or the old [*Music Academy*][4] can be installed as an extension.
Information on compatibility is available in the extension repository.

**How to install the demo:**

1. Create a new Contao installation with admin account
2. Log in as admin to the back end
3. Install the matching extension [using the extension repository][5]
4. Log out of the back end
5. Open the install tool again

To import a template, select the entry from the drop-down menu
and click the "Import template" button.

**When importing a template, existing data will be replaced!**


#### Creating an admin user

If you did not import a template, you have to create an admin user to log into
the Contao back end. After you have created the account, the installation
process is completed. The link in the lower right corner will take you to the
administration area. If you have imported the example website, you can login as
user "k.jones" with the password "kevinjones".


### Installing the Contao Demo

See *How to install the demo* in the section *Importing a template* above.


### Using search engine friendly URLs

If you are running an Apache server and are allowed to use mod_rewrite, you can
make Contao generate search engine friendly URLs that look like static HTML
documents. A set of default rewrite rules is stored in the `.htaccess.default`
file in the Contao directory. Rename this file to `.htaccess` so the Apache
server can handle it and then log into the back end and navigate to the system
settings. Select "Rewrite URLs" in the "Front end configuration" section and
save your changes. Now Contao generates static URLs like `home.html` instead of
`index.php?id=12`.


[1]: https://contao.org/en/download.html
[2]: http://www.winscp.net/
[3]: https://contao.org/en/extension-list/view/official_demo.en.html
[4]: https://contao.org/en/extension-list/view/music_academy.en.html
[5]: 05-system-administration/extensions.md#extension-catalog