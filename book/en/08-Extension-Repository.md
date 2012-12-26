# Extension Repository

To publish your own extension in the Extension Repository, you need a
[contributor's account][1]. Once you are logged in, you can access the developer
interface of the [Extension Repository][2] through the "Manage extensions" and
"Manage translations" links.


## Adding an extension

To add a new extension, follow the "Manage extensions" link and click the "Add
extension" button. You will be redirected to a form where you can enter the
extension details. The yellow box above contains important information about
naming conventions, which you should read carefully.

![](https://raw.github.com/contao/docs/2.11/book/en/images/add-extension.jpg)

The following categories are currently available:

<table>
<tr>
  <th>Category</th>
  <th>Description</th>
</tr>
<tr>
  <td>Application</td>
  <td>The extension is an autonomous application.</td>
</tr>
<tr>
  <td>Utility</td>
  <td>The extension is a utility program for the back end.</td>
</tr>
<tr>
  <td>Template</td>
  <td>The extension is a template.</td>
</tr>
<tr>
  <td>Widget</td>
  <td>The extension is a form widget.</td>
</tr>
<tr>
  <td>Plugin</td>
  <td>The extension is a PHP or JavaScript library.</td>
</tr>
<tr>
  <td>Other</td>
  <td>The extension does not fit in any of the above categories.</td>
</tr>
</table>


## Adding a release

After you have created the extension, you can add a first release. Every new
version of the extension will be stored as separate release. Open the release
manager with the respective navigation icon and click the "Add release" button.

![](https://raw.github.com/contao/docs/2.11/book/en/images/add-release.jpg)

Version numbers in the Extension Repository consist of three numeric blocks that
indicate the major, minor and maintenance version (e.g. `1.0.0`) as well as a
textual development status (e.g. `beta1`).

<table>
<tr>
  <th>Status</th>
  <th>Description</th>
</tr>
<tr>
  <td>alpha1 - alpha3</td>
  <td>Indicates that the release is an alpha version.</td>
</tr>
<tr>
  <td>beta1 - beta3</td>
  <td>Indicates that the release is a beta version.</td>
</tr>
<tr>
  <td>rc1 - rc3</td>
  <td>Indicates that the release is a release candidate.</td>
</tr>
<tr>
  <td>stable</td>
  <td>Indicates that it is a stable release for productional systems.</td>
</tr>
</table>


## Adding files

Next you have to add files to the new release. Open the file manager and click
the "Add/update files" button. You can upload single files or complete .zip
archives. Make sure to choose the correct target directory so the file paths are
correct after the upload.

![](https://raw.github.com/contao/docs/2.11/book/en/images/add-files.jpg)

![](https://raw.github.com/contao/docs/2.11/book/en/images/edit-files.jpg)


## Adding translations

Before you can publish an extension, you have to create at least one
translation. Open the translation manager and click the "Add language" button.
It is recommended to always create an English translation, because back end
users generally only see extensions in the extension manager which are available
in their language or in English (fallback language).

![](https://raw.github.com/contao/docs/2.11/book/en/images/add-translation.jpg)

![](https://raw.github.com/contao/docs/2.11/book/en/images/edit-translation.jpg)

Completed translations can be published by clicking the respective navigation
icon.


## Adding dependencies

Maybe one of your extensions uses the functionality of another one like e.g.
cron jobs. To run your extension, it is therefore required to install the cron
extension, which is usually referred to as dependency. Those dependencies can be
stored in the Extension Repository, so all required modules are installed
automatically when you install a particular extension.

![](https://raw.github.com/contao/docs/2.11/book/en/images/add-dependency.jpg)

First choose the extension that you want to add as dependency and confirm your
choice by clicking the "Continue" button. Then select the minimum and maximum
version that is known to work with your extension.


## Publishing an extension

After you have created at least one release, uploaded at least one file,
published at least one translation and added the necessary dependencies, you can
publish the extension with the respective navigation icon. Note that you cannot
remove the extension anymore once it has been published. To check if everything
works as expected, log into the back end and make a test installation with the
extension manager.


[1]: https://contao.org/en/register.html
[2]: https://contao.org/en/extension-list.html
