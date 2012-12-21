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
most likely called `htdocs`, `httpdocs`, `html` or `public_html.

[1]: https://contao.org/en/download.html
[2]: http://www.winscp.com/

If you have SSH access, you can download and extract the archive with the
following commands:

``` {.bash}
curl -L http://install.contao.org | tar -xzp
```

Now your Contao root directory should look like this:

![](images/contao-root.jpg)


## The Contao install tool

To open the Contao install tool, simply add `/contao/install.php` to the URL of
your Contao installation. Note that the install tool is protected against brute
force attacks and will be locked if a wrong password has been entered three
times in a row. To remove the lock, open file `system/config/localconfig.php` in
a text editor, find the following line and set it to `0`.

``` {.php}
$GLOBALS['TL_CONFIG']['installCount'] = 0; // This will remove the automatic lock
```

Note: In versions prior to 2.9, the path to the install tool is
`/typolight/install.php` and the default password is "typolight".


### Creating an encryption key

The encryption key is required to store encrypted data. Once encrypted, the data
can only be restored with this key, so make sure to remember it if you are using
the feature (encryption is currently not used by the Contao core modules).


### Connecting to the database

Log into your server administration panel (e.g. Plesk or Cpanel) and create a
new database for Contao. Then enter the login credentials in the Contao install
tool. Note that the Contao default character set UTF-8 is written as UTF8 in
MySQL!


### Updating database tables

Once you are connected to the database, Contao automatically checks its tables
and displays a list of recommended changes in case they are not up to date. Make
sure to read those recommendations carefully, because Contao only knows its own
tables and will try to remove those of other applications eventually sharing the
database. Confirm the changes and click the Update database button.


### Importing a template

A template is a preconfigured website that includes an example site structure
and several style sheets to format the Contao core modules and content elements.
The default template is called "Music Academy". To import it, choose
`example_website.sql` from the drop-down menu an click the Import template
button. If you have bought a commercial front end template, choose the
respective file name here. Note that any existing data will be overriden during
the template import!


### Creating an admin user

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


## Manual update


## Live Update Service


## Moving an installation


## Configuring the live server
