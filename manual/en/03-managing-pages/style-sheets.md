## Style sheets

Accessible websites should always be styled using CSS, that is why Contao
includes a "style sheets" module which allows you to manage format definitions
in the back end. To reference the various Contao elements, you need to know
their class names. [Content element classes][5] start with "ce\_"
(e.g. "ce_text") and [module classes][3] with "mod\_" (e.g. "mod_search"). If
you are not sure, simply look into the page source.

![](images/style-sheet.jpg?raw=true)

Every style sheet can be limited to one or more media types and/or to a
particular Internet Explorer version, in case you need to fix one of its
numerous bugs. Pay attention to the order of the format definitions, because
later commands override earlier ones.

```css
/* Set the general value first */
.mod_search {
    margin:24px;
}

/* Then override it for IE7 */
*:first-child+html .mod_search {
    margin:18px;
}
```

If the order was reversed, the general value would override the IE-specific
margin.


[3]: 03-managing-pages/modules.md#modules
[5]: 04-managing-content/articles.md#articles