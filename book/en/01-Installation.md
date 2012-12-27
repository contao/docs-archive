# Installation

The following chapters explain how to install and update Contao. You will learn
how to use the Contao install tool, how to synchronize an existing installation
via FTP, how to set up the Safe Mode Hack and how to configure a live server for
Contao.


## Installing Contao

First of all, download the [latest Contao archive][1] and extract it on your
local computer. Move the files into the `htdocs` folder of your local XAMPP
installation or upload them to your server with an FTP program (we recommend
using [WinSCP][2]). Depending on your server configuration, the public folder is
most likely called `htdocs`, `httpdocs`, `html` or `public_html`

If you have SSH access, you can download and extract the archive with the
following commands:

``` {.bash}
curl -L http://install.contao.org | tar -xzp
```


### The Contao install tool

To open the Contao install tool, simply add `/contao/install.php` to the URL of
your Contao installation. Note that the install tool is protected against brute
force attacks and will be locked if a wrong password has been entered three
times in a row. To remove the lock, open file `system/config/localconfig.php` in
a text editor, find the following line and set it to `0`.

``` {.php}
$GLOBALS['TL_CONFIG']['installCount'] = 0; // This will remove the automatic lock
```

<div class="note">
In versions prior to 2.9, the path to the install tool is
<code>/typolight/install.php</code> and the default password is "typolight".
</div>


#### Creating an encryption key

The encryption key is required to store encrypted data. Once encrypted, the data
can only be restored with this key, so make sure to remember it if you are using
the feature (encryption is currently not used by the Contao core modules).


#### Connecting to the database

Log into your server administration panel (e.g. Plesk or Cpanel) and create a
new database for Contao. Then enter the login credentials in the Contao install
tool. Note that the Contao default character set UTF-8 is written as `UTF8` in
MySQL!


#### Updating database tables

Once you are connected to the database, Contao automatically checks its tables
and displays a list of recommended changes in case they are not up to date. Make
sure to read those recommendations carefully, because Contao only knows its own
tables and will try to remove those of other applications eventually sharing the
database. Confirm the changes and click the Update database button.


#### Importing a template

A template is a preconfigured website that includes an example site structure
and several style sheets to format the Contao core modules and content elements.
The default template is called "Music Academy". To import it, choose
`example_website.sql` from the drop-down menu an click the Import template
button.

**Existing data will be overriden during the template import!**


#### Creating an admin user

If you did not import a template, you have to create an admin user to log into
the Contao back end. After you have created the account, the installation
process is completed. The link in the lower right corner takes you to the
administration area. If you did import the example website, you can login as
user "k.jones" with the password "kevinjones".


### Using search engine friendly URLs

If you are running an Apache server and are allowed to use mod_rewrite, you can
make Contao generate search engine friendly URLs that look like static HTML
documents. A set of default rewrite rules is stored in the `.htaccess.default`
file in the Contao directory. Rename this file to .htacess so the Apache server
can handle it and then log into the back end and edit the system settings.
Select "Rewrite URLs" in the "Front end configuration" section and save your
changes. Now Contao generates static URLs like `home.html` instead of
`index.php?id=12`.


## Using the Safe Mode Hack

While trying to install Contao with the install tool, you might have seen a
warning that the local configuration file is not writable.

![](https://raw.github.com/contao/docs/2.11/book/en/images/localconfig-not-writable.jpg)


### File permission issues

The term "Safe Mode Hack" is actually misleading, because it implies that the
problem was caused by the PHP safe_mode. However, it is caused by insufficient
file permissions and can occur even if safe_mode is disabled, so it should be
called "File Permission Hack" instead. PHP as an Apache module is typically run
as "wwwrun", "www-data" or "nobody", whereas the files that you upload via FTP
belong to you (e.g. "web4" or "ab5678"). The server therefore denies the PHP
script Contao access to those files.


#### Using FTP for file operations

To work around the permission problem, Contao establishes an FTP connection to
modify files and folders. All you have to do is to enter your FTP login details
in the local configuration file (`system/config/localconfig.php`).

``` {.php}
$GLOBALS['TL_CONFIG']['useFTP']  = true;
$GLOBALS['TL_CONFIG']['ftpHost'] = 'domain.com';
$GLOBALS['TL_CONFIG']['ftpPath'] = 'httpdocs/';
$GLOBALS['TL_CONFIG']['ftpUser'] = 'ab5678';
$GLOBALS['TL_CONFIG']['ftpPass'] = '********';
```

Replace the login details above with your own and take special care when
entering the "ftpPath", which is the relative path from the FTP root directory
to the Contao folder (e.g. `html/`, `public_html/` or `httpdocs/`). The FTP root
path is usually not the same as the document root path!


#### Setting write permissions

Obviously, the third-party plugins that are bundled with Contao are not using
the Safe Mode Hack, so you have to adjust a few folder permissions to allow
write access. Use your FTP program or SSH terminal to make the following folders
writable (CHMOD 777). Despite what you might have read in a tutorial or the
forums, only these three folders need to be modified when using the Safe Mode
Hack!

* `system/html`
* `system/logs`
* `system/tmp`

From version 2.7.3 these folder permissions should be set automatically.


#### Checking the FTP connection

To check whether you have set the correct "ftpPath", click the "Check FTP
connection" button.

![](https://raw.github.com/contao/docs/2.11/book/en/images/ftp-check.jpg)


## Manual update

When it comes to manually updating a Contao installation, you can either upload
the whole Contao download archive to the server (replacing files) or you can
upload only the files that have been modified since the last update
(synchronizing files). Either way you choose, you should always back up the
following files and folders - just in case there is an error or you accidentally
override them.

* `system/config/dcaconfig.php`
* `system/config/localconfig.php`
* `system/config/langconfig.php`
* `templates/*`
* `files/*`

This will back up your local configuration, your custom templates and your
files.


### Replacing files

Replacing the files of a Contao installation is pretty simple. Just unpack the
Contao download archive on the server or extract it on your local computer and
upload the files with an FTP client Then restore the files that you have backed
up.

**Attention:** if you have installed any third-party extensions, make sure to
backup and restore them, too, or do not overwrite them at all. Otherwise you
will have to reinstall the modules and depending on the extension you might
eventually lose data!


### Synchronizing files

To synchronize a Contao installation, you can either use the [Unix diff
utility][3] or an FTP program. Unix utilities are typically used by server
administrators only, so they will not be explained here. To synchronize files
via FTP, open WinSCP and connect to the server. Backup the files mentioned above
and then navigate to the Contao directory and click the "Synchronize files"
button.

![](https://raw.github.com/contao/docs/2.11/book/en/images/synchronization-options.jpg)

Review the options carefully and make sure to choose "Preview changes", so you
can check which files will be updated. Then confirm each file in the preview
window and doublecheck the files that are marked for deletion! Klick "OK" to
start the synchronization process.

![](https://raw.github.com/contao/docs/2.11/book/en/images/synchronization-confirmation.jpg)


### Updating the database

After you have updated the Contao files, you need to update the database, too.
Fortunately, the Contao install tool will do most of the work for you. Just open
it and enter your password, then scroll down to the database section and confirm
the changes.


## Live Update Service

The Contao Live Update Service is a commercial Contao add-on provided by [iNet
Robots][4], the company of the Contao founder and core developer, Leo Feyer. It
allows you to update your installation with a only few clicks in the back end,
without having to download a Contao archive or using an FTP program to replace
or synchronize files.

[Sign up for a Live Update ID][5]


### The update process explained

Open the Contao back end and go to the system maintenance module. Enter your
Live Update ID and click the "Run the update" button.

![](https://raw.github.com/contao/docs/2.11/book/en/images/live-update-start.jpg)


#### Choose a target version

On the next page, you can choose which Contao version you want to upgrade to. To
additionally remove deprecated resources, select "Remove deprecated core modules
and files".

![](https://raw.github.com/contao/docs/2.11/book/en/images/live-update-version-en.jpg)


#### Table of contents

The table of contents will show you the files of the update archive. Check
against this list if you have modified any core files.

![](https://raw.github.com/contao/docs/2.11/book/en/images/live-update-toc.jpg)


#### Creating a backup

Contao optionally backups the replaced files so you can easily rollback the Live
Update. The backup archives are stored in the Contao root directory, e.g.
`LU200901281100.zip` (year month day hour minute). To restore a backup, simply
unzip the archive right in place.

![](https://raw.github.com/contao/docs/2.11/book/en/images/live-update-backup.jpg)


#### Installing the update

Contao automatically creates or updates the new files and folders. Please note
that this requires write permissions. If your server requires using the Safe
Mode Hack, make sure it is configured correctly **as described in this user
guide**!

![](https://raw.github.com/contao/docs/2.11/book/en/images/live-update-files.jpg)


#### Your installation is up to date

After running the live update, your installation should be up to date.

![](https://raw.github.com/contao/docs/2.11/book/en/images/live-update-complete.jpg)


### Troubleshooting

99% of all Live Update issues are caused by wrong file permissions. Contao
requires write permissions to manage files and folders, therefore if the Live
Update does not work properly, check your server configuration and make sure to
set up the Safe Mode Hack **as described in this user guide**! Unfortunately,
there is a lot of outdated and wrong information out there.


#### Empty update archive

First of all, please note that the ZIP files in the Contao root directory
(`LU2009*.zip`) are the backup archives and not the update archives with the new
files. An empty update archive can only be recognized by an empty files list
during the update process. In this case, go to the system maintenance module and
purge the temporary folder (`system/tmp`). Then retry running the Live Update.
If you are using Contao version 2.7.0 or 2.7.1, repeat the process up to four
times if the update is not successfull.


#### How to get support

If you are having problems activating your Live Update ID or receiving the
update archive, please contact the [iNet Robots support][6]. If you are having
problems configuring the Safe Mode Hack or using Contao, please choose a support
option on the [support page][7].


## Moving an installation

Moving a Contao installation from a local server to a live server is not much
different from installing a fresh Contao version, except that you are using the
files from your local installation instead of the Contao download archive and an
SQL dump of your local database.


### Uploading the files

Open your FTP program, connect to the target server and upload all files from
your local Contao installation.


### Exporting the database

The easiest way to create a MySQL dump is to use the database administration
tool "phpMyAdmin". If you are a server administrator, you can also use the
mysqldump utility of course. Log into "phpMyAdmin", choose the database that you
want to export and click the "Export" tab in the top menu. It is important to
adjust the export settings according to the screenshot below to minimize MySQL
version compatibility problems.

![](https://raw.github.com/contao/docs/2.11/book/en/images/sql-export.jpg)


### Importing the database

Log into "phpMyAdmin" on the target server and create a new database for Contao.
Depending on the server configuration, you probably have to use the server
administration panel (e.g. "Plesk" or "Cpanel") to create new databases. Select
the empty database and click the "Import" tab in the top menu. Then upload the
SQL dump of your local database an start the import.

![](https://raw.github.com/contao/docs/2.11/book/en/images/sql-import.jpg)


### Adjusting the database configuration

Finally open the Contao install tool of the new installation (the password
should be the same as for your local installation) and adjust the database
configuration if necessary. Then go to the back end and log in with your
username and password.


## Configuring the live server

This chapter is not about configuring a server in terms of installing Apache or
compiling PHP, which you cannot do on a shared hosting account anyway. It
explains how to check whether the Contao system requirements are met and how to
enable PHP 5.


### Contao system requirements

Contao requires a webserver like Apache or IIS with PHP and MySQL support. The
minimum PHP version is 5.3.2 and the minimum MySQL version is 4.1, however we
recommend using MySQL 5 for a better performance. You also need the PHP
extensions "GDlib" (image resizing) and "SOAP" (Extension Repository) and
optionally "mbstring" (multi-byte character handling) and "mcrypt" (data
encryption). Contao has been tested successfully with all major browsers like
Firefox (from version 2) or Internet Explorer (from version 7).


### Enabling PHP 5

Fortunately, most providers meanwhile offer PHP 5, so you just have to find out
how to enable it - unless it is the default PHP version of course. If you are
lucky, your server administration panel supports switching the PHP version, in
which case you can skip to the next paragraph. If not, it most likely takes some
`.htaccess` magic to enable PHP 5. Navigate to the Contao directory and rename
the `.htaccess.default` file to `.htaccess`. Then open it in a text editor and
try one of the lines below or ask your provider which line to use.

``` {.apache}
AddHandler x-httpd-php5 .php
AddHandler php5-cgi .php
AddHandler php-cgi2 .php
AddHandler php-fastcgi5 .php
AddType x-mapp-php5 .php
AddType application/x-httpd-php5 .php
Action php /cgi-php5/php
```


### The Contao check

Download the Contao Check to find out whether your server meets the Contao
system requirements. The script will check whether you can use the Extension
Repository and the Live Update and whether you have to use the Safe Mode Hack or
not. Depending on your system configuration, you can set up a new Contao
installation with the web installer or validate an existing installation.
Extract the Zip file, upload the `check` folder to your Contao installation
directory and open it in a web browser.

[Download the Contao Check][8]
[Open the GitHub project][9]


### ISP-specific settings

There are a few major Internet Service Providers that require a little extra
configuration to get Contao to work. Fortunately, they are just the exception
from the rule. If you are looking for hassle-free Contao hosting, check out the
list of [Contao hosting partners][10].

<table>
<tr>
  <th>ISP</th>
  <th>PHP 5</th>
  <th>Safe Mode Hack</th>
  <th>Comments</th>
</tr>
<tr>
  <td>1and1</td>
  <td>Via .htaccess: <code>AddType x-mapp-php5 .php</code></td>
  <td>Required (<code>ftpPath = /</code>)</td>
  <td>&nbsp;</td>
</tr>
<tr>
  <td>allinkl.com</td>
  <td>Via .htaccess: <code>AddHandler php-fastcgi .php</code></td>
  <td>Not required</td>
  <td>PHP FastCGI is always faster than using mod_php and the Contao Safe Mode
      Hack.</td>
</tr>
<tr>
  <td>HostEurope</td>
  <td>Default</td>
  <td>Required (<code>ftpPath = www/</code>)</td>
  <td>File owner must not be "wwwrun" (can be changed in the administration
      panel "KIS").</td>
</tr>
<tr>
  <td>Strato</td>
  <td>Via .htaccess: <code>AddType application/x-httpd-php5 .php</code></td>
  <td>Not required</td>
  <td>The PHP SOAP extension is not available, so the Contao Extension
      Repository will not work.</td>
</tr>
</table>

Additional information about ISP-specific settings is available in the [Contao
forum][11].


[1]: https://contao.org/en/download.html
[2]: http://www.winscp.com/
[3]: http://en.wikipedia.org/wiki/Diff
[4]: http://www.inetrobots.com
[5]: http://www.inetrobots.com/shop/product_info.php?info=p12_Live-Update-ID.html
[6]: http://www.inetrobots.com/contact-us.html
[7]: https://contao.org/en/support.html
[8]: https://github.com/contao/check/zipball/master
[9]: https://github.com/contao/check
[10]: https://contao.org/en/partners.html?search=services&for=partner_hosting
[11]: https://community.contao.org/en/
