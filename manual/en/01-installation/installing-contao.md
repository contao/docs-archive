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

> **Warning** The URL currently refers to the latest 3.x.x version of Contao.
Therefore, you must specify the desired version by adding e.g. "/4.0.2" after the
URL. Example: curl -L http://download.contao.org/4.0.2 | tar -xzp


### Installing with Composer

You can also install Contao with Composer using the [contao/standard-edition][3]
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

First of all, before running this command, you must [install Composer][4]. It
can be installed globally with the following two commands on Mac OS X or Linux:

```bash
curl -sS https://getcomposer.org/installer | php
sudo mv composer.phar /usr/local/bin/composer
```

On Windows, you can download and run the [installer][5].

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
[CSRF][6] attacks. It is very important to take time to create a strong key. As
described in the Symfony documentation:

> **Note** Its value should be a series of characters, numbers and symbols
chosen randomly and the recommended length is around 32 characters.

You can find more information about this configuration on the
[official Symfony website][7].


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


### Folder structure

Below, a representation of the folder structure of Contao and some files
commonly used.

```bash
├── app
│   ├── AppKernel.php
│   ├── cache
│   ├── config
│   └── logs
├── assets
├── files
├── system
│   ├── config
│   │   └── localconfig.php
│   └── modules
├── templates
├── vendor
│   ├── contao
│   └── symfony
└── web
    ├── .htaccess (hidden file)
    ├── app_dev.php
    ├── app.php
    ├── install.php
    └── share
```

#### app/

This is the application folder which includes especially Symfony cache files,
Symfony configuration files and log files.


#### assets/

`assets/` contains components such as jQuery or TinyMCE. Contao CSS and JS
source files are also located in this folder as well as the combined and
minified CSS and JS files and resized images. It is available from the `web/`
folder through a symbolic link (See the [symbolic link chapter][8]).


#### files/

`files/` contains public files such as images, CSS, JavaScript, etc. It is
available from the `web/` folder through a symbolic link.


#### system/

`system/` contains Contao configuration files, the back end theme(s) and
[Contao modules][9].


#### templates/

`templates/` contains customized templates. See the [template chapter][10].


#### vendor/

This is the location of external libraries as well as the source code of Contao
and Symfony. This folder also includes Contao's [bundles][11] such as the
newsletter, the core, the news, etc. and bundles developed by the community.


#### web/

This is the web root folder that contains public files, the
[front controllers][12] and the access to the Contao install tool.

`app.php` and `app_dev.php` are the front controllers. `app.php` is used in a
production environment and all the pages requested by visitors go through this
single entry point. `app_dev.php` has the same goal as `app.php` but for a
development environment. This mode displays a toolbar with some debugging
options.

`share/` contains shared files such as XML files (e.g. sitemaps or RSS feeds).

> **Warning** For security purpose, the `web/` folder should be the only one to
be accessible by visitors.


### Symbolic link

Public files (CSS, JavaScript, images, etc.) are only available from the `web/`
folder. If some folders must be publicly available and are located outside the
`web/` folder, the system generates [symbolic links][13] (also written symlink)
for each of them. For example, the `web/assets` folder is a reference that
targets the original folder `assets` placed at the same level as the `web/`
folder.

Public files of each bundle are located in the `web/bundles` folder through
symlinks. These can be regenerated from the back end under maintenance.


### Contao modules

Existing extensions developed for Contao 3.5 and lower can be used with Contao
4 if they fulfill the compatibility requirements. You can see if an extension is
compatible by checking its `composer.json` file in the section `require` (e.g.
`contao/core-bundle":"~3.2 || ~4.1`). The procedure for installing an extension
is described in the chapter [extension][14].


[1]: https://contao.org/en/download.html
[2]: http://www.winscp.net/
[3]: https://github.com/contao/standard-edition
[4]: https://getcomposer.org/download/
[5]: https://getcomposer.org/doc/00-intro.md#using-the-installer
[6]: https://en.wikipedia.org/wiki/Cross-site_request_forgery
[7]: http://symfony.com/doc/current/reference/configuration/framework.html#secret
[8]: #symbolic-link
[9]: #contao-modules
[10]: ../04-managing-content/templates.md
[11]: http://symfony.com/doc/current/glossary.html#term-bundle
[12]: https://en.wikipedia.org/wiki/Front_Controller_pattern
[13]: https://en.wikipedia.org/wiki/Symbolic_link
[14]: ../05-system-administration/extensions.md
