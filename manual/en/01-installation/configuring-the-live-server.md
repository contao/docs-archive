## Configuring the live server

This chapter is not about configuring a server in terms of installing Apache or
compiling PHP, which you cannot do on a shared hosting account anyway. It
explains how to check whether the Contao system requirements are met and how to
enable PHP 5.


### Contao system requirements

Contao requires a webserver like Apache or IIS with PHP and MySQL support.

| Software | Version (min.) |
|----------|----------------|
| PHP      | 5.4.0          |
| MySQL    | 5.0.3          |


You also need several PHP extensions to get the full functionality.

| PHP extension | for                           | mandatory |
|---------------|-------------------------------|-----------|
| GDlib         | image resizing                | yes       |
| DOM           | XML files                     | yes       |
| SOAP          | Extension Repository          | no        |
| Phar          | Live Update                   | no        |
| mbstring      | multi-byte character handling | no        |
| mcrypt        | data encryption               | no        |

> #### info:: Note 
> Depending on your installed extensions, it may be necessary to increase the
> PHP variable `max_input_vars` (e.g. `2000` or higher). Otherwise long back end 
> forms cannot be submitted completely.

Contao has been tested successfully with all major browsers like Firefox or
Internet Explorer (from version 9).


### The Contao check

Download the Contao Check to find out whether your server meets the Contao
system requirements. The script will check whether you can use the Extension
Repository and the Live Update and whether you have to use the Safe Mode Hack or
not. Depending on your system configuration, you can set up a new Contao
installation with the web installer or validate an existing installation.

![](images/contao-check.jpg)

Extract the Zip file, upload the `check` folder to your Contao installation
directory and open it in a web browser.

[Download the Contao Check][1] | [Open the GitHub project][2]


### ISP-specific settings

There are a few major Internet Service Providers that require a little extra
configuration to get Contao to work. Fortunately, they are just the exception
from the rule. The ISP-specific settings are described in the [Contao
forum][3]. If you are looking for hassle-free Contao hosting, check out the
list of [Contao hosting partners][4].


[1]: https://github.com/contao/check/zipball/master
[2]: https://github.com/contao/check
[3]: https://community.contao.org/en/
[4]: https://contao.org/en/partners.html?search=services&for=partner_hosting
