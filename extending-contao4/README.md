# Extending Contao 4
**What's this all about?**  

This book is intended as a reference for developers. 

- We will cover several chapters on how to write or **migrate your Contao 3
  extensions** to be compatible with Contao 4.
  
- Contao 4 is the first Contao version built on the Symfony framework. We
  therefore also cover the new way of extending Contao by **writing
  Symfony bundles** in the first place.
  
- You can customize Contao a lot without even needing to develop an extension. 
  We briefly cover how to do this as well and focus on the specialties involved
  with **customizing the *Contao Managed Edition*** (in comparison to an off
  the shelf Symfony application).


**A word on building extensions for Contao 4**
   
Today, Contao is in a transition state - therefore two approaches exist on
building extensions for Contao 4:
* writing a Contao module (*the old way like in Contao 3*)
* writing a Symfony bundle *(the new way)*

The first approach is basically the same than writing an extension for
Contao 3. Thanks to the existence of a compatibility layer Contao 3 extensions
can be run in Contao 4 with minimal migration effort. If your code still needs
to support Contao 3 alongside Contao 4, this is the only option to go.  
 
The second approach is the **recommended way** for new projects. This way your
extension is ready for future Contao versions where we will slowly migrate to
use more and more Symfony components. Note that the compatibility layer is
already deprecated and will be dropped with Contao 5 as well. And - most 
important - you don't want to miss all of the cool new features that come with
Contao 4 and the Symfony ecosystem, don't you? (It's really worth it!)


> #### info:: How to?
> For a more step-by-step approach for writing a bundle, have a look in our
> [Cookbook][Cookbook]. This is also a good idea if your new to Contao or Symfony.

You can find the latest version of this document on
[docs.contao.org](https://docs.contao.org/).


{% include "SUMMARY.md" %}

{% include "LICENSE.md" %}

[Cookbook]: ../cookbook/README.md