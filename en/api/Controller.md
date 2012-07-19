
class Controller
----------------

Provide methods to manage controllers.


### Description ###

**Definition:** `abstract class Controller extends System`

**Located in:** *system/libraries/Controller.php*

**Class hierarchy:** *[System](System.php) > Controller*


### Methods ###

- *protected* [`getTheme`](Controller/getTheme.md) – Return the current theme as string
- *protected* [`getTemplate`](Controller/getTemplate.md) – Find a particular template file and return its path
- *protected* [`getTemplateGroup`](Controller/getTemplateGroup.md) – Return all template files of a particular group as array
- *protected* [`getFrontendModule`](Controller/getFrontendModule.md) – Generate a front end module and return it as HTML string
- *protected* [`getArticle`](Controller/getArticle.md) – Generate an article and return it as string
- *protected* [`getContentElement`](Controller/getContentElement.md) – Generate a content element and return it as HTML string
- *protected* [`getForm`](Controller/getForm.md) – Generate a form and return it as HTML string
- *protected* [`getPageDetails`](Controller/getPageDetails.md) – Get the details of a page including inherited parameters and return it as object
- *protected* [`getPageSections`](Controller/getPageSections.md) – Return all page sections as array
- *protected* [`getLanguages`](Controller/getLanguages.md) – Return all languages as array
- *protected* [`getBackendLanguages`](Controller/getBackendLanguages.md) – Return an array of supported back end languages
- *public* [`getBackendThemes`](Controller/getBackendThemes.md) – Return all back end themes as array
- *protected* [`getCountries`](Controller/getCountries.md) – Return all counties as array
- *protected* [`getTimeZones`](Controller/getTimeZones.md) – Return all timezones as array
- *protected* [`resizeImage`](Controller/resizeImage.md) – Resize or crop an image
- *protected* [`getImage`](Controller/getImage.md) – Resize an image
- *protected* [`getSpellcheckerString`](Controller/getSpellcheckString.md) – Return the current languages to be used with the TinyMCE spellchecker
- *protected* [`printArticleAsPdf`](Controller/printArticleAsPdf.md) – Print an article as PDF and stream it to the browser
- *protected* [`replaceInsertTags`](Controller/replaceInsertTags.md) – Replace insert tags with their values
- *protected* [`restoreBasicEntities`](Controller/restoreBasicEntities.md) – Restore basic entities
- *protected* [`parseSimpleTokens`](Controller/parseSimpleTokens.md) – Parse simple tokens that can be used to personalize newsletters
- *protected* [`generateImage`](Controller/generateImage.md) – Generate an image tag and return it as HTML string
- *protected* [`generateMargin`](Controller/generateMargin.md) – Take an array of four margin values and the current unit and compile the margin style definition
- *protected* [`generateFrontendUrl`](Controller/generateFrontendUrl.md) – Generate an URL from a tl_page record depending on the current rewriteURL setting and return it
- *protected* [`convertRelativeUrls`](Controller/convertRelativeUrls.md) – Convert relative URLs to absolute URLs
- *protected* [`sendFileToBrowser`](Controller/sendFileToBrowser.md) – Send a file to the browser so the "save as" dialogue opens
- *protected* [`loadDataContainer`](Controller/loadDataContainer.md) – Load a set of DCA files
- *protected* [`prepareForWidget`](Controller/prepareForWidget.md) – Convert a back end DCA so it can be used with the widget class
- *protected* [`createInitialVersion`](Controller/createInitialVersion.md) – Create an initial version of a record
- *protected* [`createNewVersion`](Controller/createNewVersion.md) – Create a new version of a record
- *protected* [`redirectToFrontendPage`](Controller/redirectToFrontendPage.md) – Redirect to a front end page
- *protected* [`getChildRecords`](Controller/getChildRecords.md) – Return the IDs of all child records of a particular record
- *protected* [`classFileExists`](Controller/classFileExists.md) – Return true if a class file exists
- *protected* [`eliminateNestedPaths`](Controller/eliminateNestedPaths.md) – Take an array of paths and eliminate nested paths
- *protected* [`eliminateNestedPages`](Controller/eliminateNestedPages.md) – Take an array of pages and eliminate nested pages
- *protected* [`optionSelected`](Controller/optionSelected.md) – Return a "selected" attribute if the current option is selected
- *protected* [`optionChecked`](Controller/optionChecked.md) – Return a "checked" attribute if the current option is checked
- *protected* [`findContentElement`](Controller/findContentElement.md) – Find a content element in the TL_CTE array and return its value
- *protected* [`findFrontendModule`](Controller/findFrontendModule.md) – Find a front end module in the FE_MOD array and return its value
- *protected* [`removeOldFeeds`](Controller/removeOldFeeds.md) – Remove old XML files from the root directory
- *protected* [`addImageToTemplate`](Controller/addImageToTemplate.md) – Add an image to a template
- *protected* [`addEnclosuresToTemplate`](Controller/addEnclosuresToTemplate.md) – Add enclosures to a template
- *protected* [`setStaticUrl`](Controller/setStaticUrl.md) – Set a static URL constant and replace the protocol when requested via SSL
- *protected* [`addStaticUrlTo`](Controller/addStaticUrlTo.md) – Add a static URL to a script
