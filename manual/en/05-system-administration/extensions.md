## Extensions

Extensions are an essential part of Contao, because they allow you to add extra
functionality. There are more than 1,400 extensions available in the Contao
Extension Repository, which you can browse directly in the back end.
Communication with the repository server is done via SOAP, so you need to enable
the PHP SOAP extension to use the service (if not enabled by default).


### Extension catalog

The "extension catalog" module allows you to browse the extension list and to
install extensions at the push of a button. Use the filter and sorting options
to find a particular extension and click the info icon or extension title to
open the details page and install the module.

![](images/extension-list.jpg?raw=true)

The details page contains a description of the extension and important
information regarding system requirements, versions and dependencies from other
modules. Click the "Install" button to download and install the extension.

![](images/extension-details.jpg?raw=true)

Contao will automatically download and install the extension and update the
database if necessary.

![](images/extension-install.jpg?raw=true)


### Extension manager

The "extension manager" module allows you to update and uninstall extensions. It
automatically checks for updates and notifies you if a new version is available.
Many extensions also include links to an online manual and/or forum thread where
you can get support.

![](images/extension-manager.jpg?raw=true)

To uninstall an extension, simply click the uninstall icon and follow the
instructions. The extension manager will remove all files and folders and update
the database if necessary. Note that this action cannot be undone and the tables
cannot be restored!

![](images/extension-uninstall.jpg?raw=true)


### Manual installation

In case the PHP SOAP extension is not available on your server, you can also
install Contao extensions manually. Find the respective module in the [extension
list][1] and download the .zip archive of the latest release. Then unzip the
files and copy them to your local or remote Contao directory. Finally, check the
database with the [Contao install tool][2].


[1]: https://contao.org/en/extension-list.html
[2]: ../01-installation/installing-contao.md#the-contao-install-tool