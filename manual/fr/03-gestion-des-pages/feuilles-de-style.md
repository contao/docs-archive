## Feuilles de style

Les sites internet accessibles doivent toujours être formatés à l'aide des CSS,
c'est pourquoi Contao inclut un module "feuilles de style" qui vous permet de
gérer les définitions de formatage dans le back office. Pour référencer les
différents éléments de Contao, vous devez connaître leurs noms de classe. Les
[classes des éléments de contenu][1] commencent par "ce\_" (par exemple
"ce\_text") et les [classes des modules][2] avec "mod\_"
(par exemple "mod\_search"). Si vous n'êtes pas sûr, il suffit de
regarder dans le code source de la page.

![](images/feuille-de-style.jpg)

Chaque feuille de style peut être limitée par un ou plusieurs types de média
et/ou par une version particulière d'Internet Explorer, dans le cas où vous avez
besoin de fixer un de ses nombreux bogues. Faites attention à l'ordre des
définitions de formatage, car celles qui suivent, remplacent les précédentes.

```css
/* Définir la valeur générale d'abord */
.mod_search {
    margin:24px;
}

/* Puis la remplacer pour IE7 */
*:first-child+html .mod_search {
    margin:18px;
}
```

Si l'ordre est inversé, la valeur générale l'emporterait sur la marge spécifique
à Internet Explorer.


[1]: ../04-gestion-du-contenu/articles.md#articles
[2]: ../03-gestion-des-pages/modules.md#modules
