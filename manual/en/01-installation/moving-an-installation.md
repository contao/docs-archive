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
`mysqldump` utility of course. Log into "phpMyAdmin", choose the database that
you want to export and click the "Export" tab in the top menu. It is important
to adjust the export settings according to the screenshot below to minimize
MySQL version compatibility problems.

![](images/sql-export.jpg)


### Importing the database

Open "phpMyAdmin" on the target server and create a new database for Contao.
Depending on the server configuration, you probably have to use the server
administration panel (e.g. "Plesk" or "cPanel") to create new databases. Select
the empty database and click the "Import" tab in the top menu. Then upload the
SQL dump of your local database and start the import.

![](images/sql-import.jpg)


### Adjusting the database configuration

Finally open the Contao install tool of the new installation (the password
should be the same as for your local installation) and adjust the database
configuration if necessary. Then go to the back end and log in with your
username and password.
