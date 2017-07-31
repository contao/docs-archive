# Bundles for Contao

Follow the next steps if your bundle is designed specifically for Contao.


## Package type
 
Make sure the type in your bundle's ``composer.json``is set to ``contao-bundle``.
This way it can be associated with Contao.  

```json
{
  "name": "vendor/contao-something",
  "type": "contao-bundle",
  
  "require": {
    "contao/core-bundle": "^4.4"
  }
  
  // [...]
}
```


## Manager Plugin

Add a *Manager Plugin* so that your bundle can run in a *Contao Managed Edition*.  
→ [Writing a Manager Plugin](../managed-edition/plugins.md)


## Help making Contao even better
We love seeing you share your reusable bundles with the community. If you do so
make sure to also add your bundle to [Packagist][Packagist] (Composers default
place to get packages from). It's a quick and easy step but makes working with
your bundle so much easier. 



[Packagist]: https://packagist.org/