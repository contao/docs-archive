
class Controller
----------------

Provide methods to manage controllers.


### Description ###

**Definition:** `abstract class Controller extends System`

**Located in:** *system/libraries/Controller.php*

**Class hierarchy:** *[System](System.php) > Controller*


### Methods ###

- *protected* `getTheme` – Return the current theme as string
- *protected* `getTemplate` – Find a particular template file and return its path
- *protected* `getTemplateGroup` – Return all template files of a particular group as array
- *protected* `getFrontendModule` – Generate a front end module and return it as HTML string
- *protected* `getArticle` – Generate an article and return it as string
- *protected* `getContentElement` – Generate a content element and return it as HTML string
- *protected* `getForm` – Generate a form and return it as HTML string
- *protected* `getPageDetails` – Get the details of a page including inherited parameters and return it as object
- *protected* `getPageSections` – Return all page sections as array
- *protected* `getLanguages` – Return all languages as array
- *protected* `getBackendLanguages` – Return an array of supported back end languages
- *public* `getBackendThemes` – Return all back end themes as array
- *protected* `getCountries` – Return all counties as array
- *protected* `getTimeZones` – Return all timezones as array
- *protected* `resizeImage` – Resize or crop an image
- *protected* [`getImage`](Controller/getImage.md) – Resize an image
- *protected* `getSpellcheckerString` – Return the current languages to be used with the TinyMCE spellchecker
- *protected* `printArticleAsPdf` – Print an article as PDF and stream it to the browser
- *protected* `replaceInsertTags` – Replace insert tags with their values
- *protected* `restoreBasicEntities` – Restore basic entities
- *protected* `parseSimpleTokens` – Parse simple tokens that can be used to personalize newsletters
- *protected* `generateImage` – Generate an image tag and return it as HTML string
- *protected* `generateMargin` – Take an array of four margin values and the current unit and compile the margin style definition
- *protected* [`generateFrontendUrl`](Controller/generateFrontendUrl.md) – Generate an URL from a tl_page record depending on the current rewriteURL setting and return it
- *protected* `convertRelativeUrls` – Convert relative URLs to absolute URLs
- *protected* `sendFileToBrowser` – Send a file to the browser so the "save as" dialogue opens
- *protected* `loadDataContainer` – Load a set of DCA files
- *protected* `prepareForWidget` – Convert a back end DCA so it can be used with the widget class
- *protected* `createInitialVersion` – Create an initial version of a record
- *protected* `createNewVersion` – Create a new version of a record
- *protected* `redirectToFrontendPage` – Redirect to a front end page
- *protected* `getChildRecords` – Return the IDs of all child records of a particular record (see #2475)
- *protected* `classFileExists` – Return true if a class file exists
- *protected* `eliminateNestedPaths` – Take an array of paths and eliminate nested paths
- *protected* `eliminateNestedPages` – Take an array of pages and eliminate nested pages
- *protected* `optionSelected` – Return a "selected" attribute if the current option is selected
- *protected* `optionChecked` – Return a "checked" attribute if the current option is checked
- *protected* `findContentElement` – Find a content element in the TL_CTE array and return its value
- *protected* `findFrontendModule` – Find a front end module in the FE_MOD array and return its value
- *protected* `removeOldFeeds` – Remove old XML files from the root directory
- *protected* `addImageToTemplate` – Add an image to a template
- *protected* `addEnclosuresToTemplate` – Add enclosures to a template
- *protected* `setStaticUrl` – Set a static URL constant and replace the protocol when requested via SSL
- *protected* `addStaticUrlTo` – Add a static URL to a script
