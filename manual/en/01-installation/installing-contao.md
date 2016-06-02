## Installing Contao

First of all, download the [latest Contao archive][1] and extract it on your
local computer. Move the files into the `htdocs` folder of your local
installation (e.g. XAMPP) or upload them to your server with an FTP program (we
recommend using [WinSCP][2]). Make sure to upload the hidden `.htaccess.default`
file and replace its name with `.htaccess`. Depending on your server
configuration, the public folder is most likely called `htdocs`, `httpdocs`,
`html` or `public_html`.

If you have SSH access, you can download and extract the archive with the
following commands:

```bash
curl -L http://download.contao.org | tar -xzp
```

> **Warning** The URL currently refers to the latest 3.x.x version of Contao.
Therefore, you must specify the desired version by adding e.g. "/4.0.2" after the
URL. Example: curl -L http://download.contao.org/4.0.2 | tar -xzp


### Installing with Composer

You can also install Contao with Composer using the [contao/standard-edition][6]
repository.

```bash
php composer.phar create-project contao/standard-edition <target>
```

You have to replace the `<target>` parameter with a path to a folder where the
Contao files will be created. If the target folder does not exist, it will be
created automatically.

> **Info** The command above always installs the latest stable version. If you
want to install a specific version, you must insert it in the command as for
example: `php composer.phar create-project contao/standard-edition:4.0.2 <target>`

> **Info** On Windows, you must run this command as an administrator.

First of all, before running this command, you must [install Composer][7]. It
can be installed globally with the following two commands on Mac OS X or Linux:

```bash
curl -sS https://getcomposer.org/installer | php
sudo mv composer.phar /usr/local/bin/composer
```

On Windows, you can download and run the [installer][10].

During the installation in your command-line interface, you must assign a value
to a number of parameters:

```bash
Some parameters are missing. Please provide them.
database_host (localhost):
database_port (3306):
database_user (null):
database_password (null):
database_name (null):
mailer_transport (mail):
mailer_host (127.0.0.1):
mailer_user (null):
mailer_password (null):
mailer_port (25):
mailer_encryption (null):
prepend_locale (false):
secret (ThisTokenIsNotSoSecretChangeIt):
```

Default values are listed in parentheses. All these data will be included in the
configuration file `app/config/parameters.yml`.

The `secret` parameter allows you to create a key that will be used against
[CSRF][8] attacks. It is very important to take time to create a strong key. As
described in the Symfony documentation:

> **Note** Its value should be a series of characters, numbers and symbols
chosen randomly and the recommended length is around 32 characters.

You can find more information about this configuration on the
[official Symfony website][9].


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

> **Danger** When importing a template, existing data will be replaced!


#### Creating an admin user

If you did not import a template, you have to create an admin user to log into
the Contao back end. After you have created the account, the installation
process is completed. The link in the lower right corner will take you to the
administration area.


[1]: https://contao.org/en/download.html
[2]: http://www.winscp.net/
[6]: https://github.com/contao/standard-edition
[7]: https://getcomposer.org/download/
[8]: https://en.wikipedia.org/wiki/Cross-site_request_forgery
[9]: http://symfony.com/doc/current/reference/configuration/framework.html#secret
[10]: https://getcomposer.org/doc/00-intro.md#using-the-installer
