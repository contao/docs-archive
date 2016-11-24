# Contao 4 – Managed Edition

Starting with version 4.3, Contao is available as a so-called *Managed Edition*.
 Compared to a regular Symfony application, a *Managed Edition* is limited
 in it's customization possibilities to allow automatic management by third-party
 bundles.
 

## Differences to Symfony Standard


### AppKernel

Contao *Managed Edition* does not feature an `AppKernel` class that can be
customized. Bundles are automatically loaded by *Plugins* so users do not need
to know how to write PHP code or what classes to instantiate in what order.


### Config files

Contao *Managed Edition* does not feature the regular Symfony config files
in `app/config`. Instead, all configurations are loaded by bundles using the
Symfony *[Prepend configuration]* interface.



[Prepend configuration]: http://symfony.com/doc/current/bundles/prepend_extension.html
