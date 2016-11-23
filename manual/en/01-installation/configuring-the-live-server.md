## Configuring the live server

This chapter is not about configuring a server in terms of installing Apache or
compiling PHP, which you cannot do on a shared hosting account anyway. It
explains how to check whether the Contao system requirements are met and how to
enable PHP 5.


### Contao system requirements

Contao requires a webserver like Apache or IIS with PHP and MySQL support.

| Software | Version (min.) |
|----------|----------------|
| PHP      | 5.5.0          |
| MySQL    | 5.0.3          |


You also need several PHP extensions to get the full functionality.

| PHP extension | for                           | mandatory |
|---------------|-------------------------------|-----------|
| GDlib         | image resizing                | yes       |
| DOM           | XML files                     | yes       |
| intl          | Internationalization          | yes       |
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
system requirements.

![](images/contao-check.jpg)

Extract the Zip file, upload the `check` folder to your Contao installation
directory and open it in a web browser.

[Download the Contao Check][1] | [Open the GitHub project][2]

> #### info:: Note
> You cannot validate a Contao 4 installation with the Contao Check.


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
