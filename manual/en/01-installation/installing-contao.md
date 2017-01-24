## Installing Contao

First of all, download the [latest Contao archive][1] and extract it on your
local computer. Move the files into the `htdocs` folder of your local
installation (e.g. XAMPP) or upload them to your server with an FTP program (we
recommend using [WinSCP][2]). Depending on your server configuration, the public
folder is most likely called `htdocs`, `httpdocs`, `html`, `public_html` or `www`.

If you have SSH access to your server, you can download and extract the 
archive directly on the command line, e.g. with `curl`. Depending on the
version you want to install, adjust the URLs as described.

Latest version of Contao (4.x):
```bash
curl -L http://download.contao.org | tar -xzp
```

<abbr title="Long Term Support">LTS</abbr> version of Contao (3.5):
```bash
curl -L http://download.contao.org/lts | tar -xzp
```

A specific version (e.g. 3.5.2):
```bash
curl -L http://download.contao.org/3.5.2 | tar -xzp
```


### Installing with Composer

You can also install Contao with Composer using the [contao/standard-edition][3]
repository.

First of all, you must [install Composer][4]. It can be installed globally with
the following two commands on macOS or Linux:

```bash
curl -sS https://getcomposer.org/installer | php
sudo mv composer.phar /usr/local/bin/composer
```

On Windows, you can download and run the [installer][5].

Now, you can run the installation process of Contao with the following command:

```bash
composer create-project contao/standard-edition <target>
```

You have to replace the `<target>` parameter with a path to a folder where the
Contao files will be created. If the target folder does not exist, it will be
created automatically.

> #### info:: Note
> The command above always installs the latest stable version. If you
> want to install a specific version, you must insert it in the command as for
> example: `composer create-project contao/standard-edition:4.1.3 <target>`

<!-- Quote break -->

> #### info:: Note
> On Windows, depending on the setup (e.g. default XAMPP), you might need run
> this command as an administrator.

During the installation in your command-line interface, you must assign a value
to a number of parameters:

```
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
```

Default values are listed in parentheses. All these data will be included in the
configuration file `app/config/parameters.yml`.

> #### info:: Note
> In the version 4.2 and higher, the `secret` parameter is
> automatically generated during the installation. You can find more information
> about this configuration on the [official Symfony website][6].


### The document root

In production, make sure to specify the `web/` directory as the document root
of your website (e.g. using the admin panel of your web hosting provider).

> #### info:: Note
> More detailed information relating to the folder structure can be found in
> this [cookbook chapter][7].


### The Contao install tool

To open the Contao install tool, simply add `/contao/install` to the URL of
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

> #### danger:: Danger
> When importing a template, existing data will be replaced!


#### Creating an admin user

If you did not import a template, you have to create an admin user to log into
the Contao back end. After you have created the account, the installation
process is completed. The link in the lower right corner will take you to the
administration area.


[1]: https://contao.org/en/download.html
[2]: http://www.winscp.net/
[3]: https://github.com/contao/standard-edition
[4]: https://getcomposer.org/download/
[5]: https://getcomposer.org/doc/00-intro.md#using-the-installer
[6]: http://symfony.com/doc/current/reference/configuration/framework.html#secret
[7]: https://docs.contao.org/books/cookbook/en/folder-structure.html