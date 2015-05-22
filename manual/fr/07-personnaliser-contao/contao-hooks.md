## Contao hooks

Les hooks fonctionnent de la même manière que les [fonctions callback][1] du
tableau conteneur de données (DCA). Vous pouvez enregistrer une ou plusieurs
fonctions pour un événement donné, et lorsque l'événement est déclenché, les
fonctions callback sont exécutées. Les hooks vous permettent d'ajouter des
fonctionnalités personnalisées au cœur de Contao.


### activateAccount

Le hook `activateAccount` est déclenché lorsqu'un nouveau compte en front
office est activé. Il passe l'objet User en argument et n'attend pas de
valeur de retour. Il est disponible à partir de la version 2.4.3.

```php
// config.php
$GLOBALS['TL_HOOKS']['activateAccount'][] = array('MyClass',
'myActivateAccount');

// MyClass.php
public function myActivateAccount(Database_Result $objUser)
{
    // Faire quelque chose
}
```


### activateRecipient

Le hook `activateRecipient` est déclenché lorsqu'un nouveau destinataire d'une
newsletter est ajouté. Il passe l'adresse e-mail, les ID du destinataire et de
la liste de diffusion en arguments et n'attend pas de valeur de retour. Il est
disponible à partir de la version 2.8.RC1.

```php
// config.php
$GLOBALS['TL_HOOKS']['activateRecipient'][] = array('MyClass',
'myActivateRecipient');

// MyClass.php
public function myActivateRecipient($strEmail, $arrRecipients, $arrChannels)
{
    // Faire quelque chose
}
```


### addComment

Le hook `addComment` est déclenché lorsqu'un commentaire est ajouté. Il passe
l'ID de l'enregistrement et le tableau de données en arguments et n'attend pas
de valeur de retour. Il est disponible à partir de la version 2.8.2.

```php
// config.php
$GLOBALS['TL_HOOKS']['addComment'][] = array('MyClass', 'myAddComment');

// MyClass.php
public function myAddComment($intId, $arrSet)
{
    // Faire quelque chose
}
```


### addCustomRegexp

Le hook `addCustomRegexp` est déclenché lorsqu'une expression régulière inconnue
est trouvée. Il passe le nom de l'expression régulière, la valeur courante et
l'objet Widget en arguments et attend une valeur de retour de type booléen. Il
est disponible à partir de la version 2.6.2.

```php
// config.php
$GLOBALS['TL_HOOKS']['addCustomRegexp'][] = array('MyClass',
'myAddCustomRegexp');

// MyClass.php
public function myAddCustomRegexp($strRegexp, $varValue, Widget $objWidget)
{
    if ($strRegexp == 'postal')
    {
        if (!preg_match('/^0-9{4,6}$/', $varValue))
        {
            $objWidget->addError('Field ' . $objWidget->label . ' should be a postal code.');
        }

        return true;
    }

    return false;
}
```


### addLogEntry

Le hook `addLogEntry` est déclenché lorsqu'une nouvelle entrée est ajoutée au
journal (log). Il passe le message, la fonction et l'action en arguments et
n'attend pas de valeur de retour. Il est disponible à partir de la version
2.8.RC1.

```php
// config.php
$GLOBALS['TL_HOOKS']['addLogEntry'][] = array('MyClass', 'myAddLogEntry');

// MyClass.php
public function myAddLogEntry($strText, $strFunction, $strAction)
{
    // Faire quelque chose
}
```


### checkCredentials

Le hook `checkCredentials` est déclenché lorsqu'une tentative d'identification
échoue à cause d'un mot de passe incorrect. Il passe le nom de l'utilisateur,
le mot de passe et l'objet User en arguments et attend une valeur de
retour de type booléen. Il est disponible à partir de la version 2.6.0.

```php
// config.php
$GLOBALS['TL_HOOKS']['checkCredentials'][] = array('MyClass',
'myCheckCredentials');

// MyClass.php
public function myCheckCredentials($strUsername, $strPassword, User $objUser)
{
    // Check against a global database
    if ($this->checkGlobalDbFor($strUsername, $strPassword))
    {
        return true;
    }

    return false;
}
```


### closeAccount

Le hook `closeAccount` est déclenché lorsqu'un utilisateur clôture son compte.
Il passe l'ID de l'utilisateur, le mode opérationnel et le module en arguments
et n'attend pas de valeur de retour. Il est disponible à partir de la version
2.8.0.

```php
// config.php
$GLOBALS['TL_HOOKS']['closeAccount'][] = array('MyClass', 'myCloseAccount');

// MyClass.php
public function myCloseAccount($intId, $strMode, $objModule)
{
    if ($strMode == 'close_delete')
    {
        // Faire quelque chose
    }
}
```


### compileDefinition

Le hook `compileDefinition` est déclenché quand une définition de formatage
d'une feuille de style est écrite. Il passe le tableau de configuration en
argument et attend une chaîne de caractères comme valeur de retour. Il est
disponible à partir de la version 2.9.4.

```php
// config.php
$GLOBALS['TL_HOOKS']['compileDefinition'][] = array('MyClass',
'myCompileDefinition');

// MyClass.php
public function myCompileDefinition($arrRow)
{
    if (isset($arrRow['border-radius']))
    {
        return "\nborder-radius:" . $arrRow['border-radius'] . ";";
    }

    return '';
}
```


### compileFormFields

Le hook `compileFormFields` est déclenché avant qu'un champ de formulaire soit
chargé. Il passe un tableau d'objets FormFieldModel ainsi que l'ID et l'objet
du formulaire en arguments et attend le tableau d'objets FormFieldModel comme
valeur de retour. Avec ce hook, les champs de formulaire peuvent être ajustés
dynamiquement avant l'affichage. Il est disponible à partir de la version 3.2.

```php
// config.php
$GLOBALS['TL_HOOKS']['compileFormFields'][] = array('MyClass', 'myCompileFormFields');

// MyClass.php
public function myCompileFormFields($arrFields, $formId, $this)
{
    if ($formId == 'my_form_id')
    {
        foreach ($arrFields AS $objFields)
        {
    if($objFields->name == 'my_form_field_1')
    {
      // Faire quelque chose
          }
  }
    }

    return $arrFields;
}
```


### createDefinition

Le hook `createDefinition` est déclenché quand une définition de formatage
d'une feuille de style est importée. Il passe la clé et la valeur, la définition
de formatage d'origine et le tableau de données en arguments et attend un
tableau ou `false` comme valeur de retour. Il est disponible à partir de la
version 2.9.4.

```php
// config.php
$GLOBALS['TL_HOOKS']['createDefinition'][] = array('MyClass',
'myCreateDefinition');

// MyClass.php
public function myCreateDefinition($strKey, $strValue, $strDefinition, $arrSet)
{
    if ($strKey == 'border-radius')
    {
        return array('border-radius'=>$strValue);
    }

    return false;
}
```


### createNewUser

Le hook `createNewUser` est déclenché lorsqu'un nouvel utilisateur front office
s'enregistre sur le site internet. Il passe le nouvel utilisateur et le tableau
de données en arguments et n'attend pas de valeur de retour. Il est disponible à
partir de la version 2.2.0.

```php
// config.php
$GLOBALS['TL_HOOKS']['createNewUser'][] = array('MyClass', 'myCreateNewUser');

// MyClass.php
public function myCreateNewUser($intId, $arrData)
{
    // Modification de l'enregistrement
}
```


### executePreActions

Le hook `executePreActions` est déclenché par les requêtes Ajax qui ne
nécessitent pas un objet DCA. Il passe le nom de l'action en argument et n'attend
pas de valeur de retour. Il est disponible à partir de la version 2.6.1.

```php
// config.php
$GLOBALS['TL_HOOKS']['executePreActions'][] = array('MyClass', 'myExecutePreActions');

// MyClass.php
public function myExecutePreActions($strAction)
{
    if ($strAction == 'update')
    {
        // Faire quelque chose
    }
}
```


### executePostActions

Le hook `executePostActions` est déclenché par les requêtes Ajax qui nécessitent
un objet DCA. Il passe le nom de l'action et l'objet DataContainer en arguments
et n'attend pas de valeur de retour. Il est disponible à partir de la
version 2.6.1.

```php
// config.php
$GLOBALS['TL_HOOKS']['executePostActions'][] = array('MyClass', 'myExecutePostActions');

// MyClass.php
public function myExecutePostActions($strAction, DataContainer $dc)
{
    if ($strAction == 'update')
    {
        // Faire quelque chose
    }
}
```


### generateBreadcrumb

Le hook `generateBreadcrumb` permet de modifier la navigation fil d'Ariane. Il
passe les éléments de navigation et le module front office en arguments et
attend des éléments comme valeur de retour. Il est disponible à partir de la
version 2.10.0.

```php
// config.php
$GLOBALS['TL_HOOKS']['generateBreadcrumb'][] = array('MyClass', 'myGenerateBreadcrumb');

// MyClass.php
public function myGenerateBreadcrumb($arrItems, \Module $objModule)
{
  return $arrItems;
}
```


### generateFrontendUrl

Le hook `generateFrontendUrl` est déclenché lors de la re-création d'une URL
de front office. Il passe l'objet Page, la chaîne de paramètres et l'URL par
défaut en arguments et attend une chaîne de caractères comme valeur de retour.
Il est disponible à partir de la version 2.5.8.

```php
// config.php
$GLOBALS['TL_HOOKS']['generateFrontendUrl'][] = array('MyClass', 'myGenerateFrontendUrl');

// MyClass.php
public function myGenerateFrontendUrl($arrRow, $strParams, $strUrl)
{
    return str_replace('.html', '.xml', $strUrl);
}
```


### generatePage

Le hook `generatePage` est déclenché avant la compilation du modèle de
présentation principale ("fe_page"). Il passe l'objet Page, l'objet Model
et une référence qui lui est propre en arguments et n'attend pas de valeur
de retour. Il est disponible à partir de la version 2.8.RC1.


```php
// config.php
$GLOBALS['TL_HOOKS']['generatePage'][] = array('MyClass', 'myGeneratePage');

// MyClass.php
public function myGeneratePage(\PageModel $objPage, \LayoutModel $objLayout, \PageRegular $objPageRegular)
{
    // Faire quelque chose
}
```


### getAllEvents

Le hook `getAllEvents` vous permet de modifier les jeux de résultats produits
par les modules calendrier et événements. Il passe le jeu de résultats courant,
les ID des éléments parents et l'heure de début et de fin en arguments et
attend un jeu de résultats (tableau) comme valeur de retour. Il est disponible
à partir de la version 2.6.4.

```php
// config.php
$GLOBALS['TL_HOOKS']['getAllEvents'][] = array('MyClass', 'myGetAllEvents');

// MyClass.php
public function myGetAllEvents($arrEvents, $arrCalendars, $intStart, $intEnd, Module $objModule)
{
    ksort($arrEvents);
    return $arrEvents;
}
```


### getContentElement

Le hook `getContentElement` est déclenché lorsqu'un élément de contenu est
rendu. Il passe l'objet Database et une chaîne-tampon (buffer string) en
arguments et attend une chaîne-tampon comme valeur de retour. Il est disponible
à partir de la version 2.9.0.

```php
// config.php
$GLOBALS['TL_HOOKS']['getContentElement'][] = array('MyClass', 'myGetContentElement');

// MyClass.php
public function myGetContentElement(Database_Result $objElement, $strBuffer)
{
    return $strBuffer;
}
```


### getImage

Le hook `getImage` est déclenché quand une vignette est générée et vous permet
d'ajouter une routine personnalisée. Il passe le chemin d'accès, la largeur et
la hauteur, la mode, le nom du cache et l'objet File en arguments et attend
un chemin d'accès comme valeur de retour. Il est disponible à partir de la
version 2.8.RC1.

```php
// config.php
$GLOBALS['TL_HOOKS']['getImage'][] = array('MyClass', 'myGetImage');

// MyClass.php
public function myGetImage($image, $width, $height, $mode, $strCacheName, $objFile)
{
    return MyImage::generateThumbnail($image, $widht, $height, $mode);
}
```


### getPageIdFromUrl

Le hook `getPageIdFromUrl` est déclenché lors de l'évaluation des parties d'une
URL. Il passe les fragments d'URL en argument et attend un tableau de fragments
d'une URL en valeur de retour. Il est disponible depuis la version 2.5.4.

```php
// config.php
$GLOBALS['TL_HOOKS']['getPageIdFromUrl'][] = array('MyClass', 'myGetPageIdFromUrl');

// MyClass.php
public function myGetPageIdFromUrl($arrFragments)
{
    return array_unique($arrFragments);
}
```


### getPageLayout

Le hook `getPageLayout` est exécutée avant d'initialiser le modèle front office.
Il passe le modèle de la page, l'objet Model et une référence à l'objet Page en
arguments et n'attend pas de valeur de retour. Il est disponible à partir de la
version 3.1.0.

```php
// config.php
$GLOBALS['TL_HOOKS']['getPageLayout'][] = array('MyClass', 'mygetPageLayout');

// MyClass.php
public function mygetPageLayout(\PageModel $objPage, \LayoutModel $objLayout, \PageRegular $objPageRegular)
{
    // Faire quelque chose
}
```


### getSearchablePages

Le hook `getSearchablePages` est déclenché lors de la reconstruction de l'index
de recherche. Il passe le tableau des pages et l'ID de la page racine en
arguments et attend un tableau d'URLs absolues (!) comme valeur de retour. Il
est disponible à partir de la version 2.2.0.

```php
// config.php
$GLOBALS['TL_HOOKS']['getSearchablePages'][] = array('MyClass', 'myGetSearchablePages');

// MyClass.php
public function myGetSearchablePages($arrPages, $intRoot)
{
    return array_merge($arrPages, array('Additional pages'));
}
```


### initializeSystem

Le hook `initializeSystem` est déclenché lorsque le système est initialisé. Il
est disponible à partir de la version 3.1.RC1.

```php
// config.php
$GLOBALS['TL_HOOKS']['initializeSystem'][] = array('MyClass', 'myInitializeSystem');

// MyClass.php
public function myInitializeSystem()
{
    // Faire quelque chose
}
```


### importUser

Le hook `importUser` est déclenché lorsqu'un nom d'utilisateur ne peut être
trouvé dans la base de données. Il passe le nom d'utilisateur, le mot de passe
et le nom de la table en arguments et attend une valeur de retour de type
booléen. Il est disponible à partir de la version 2.7.RC1.

```php
// config.php
$GLOBALS['TL_HOOKS']['importUser'][] = array('MyClass', 'myImportUser');

// MyClass.php
public function myImportUser($strUsername, $strPassword, $strTable)
{
    if ($strTable == 'tl_member')
    {
        // Importe l'utilisateur à partir d'un serveur LDAP
        if ($this->importUserFromLdap($strUsername, $strPassword))
        {
            return true;
        }
    }

    return false;
}
```


### isVisibleElement

Le hook `isVisibleElement` est déclenché lors de la vérification si un élément
doit être visible dans le front office ou non. Un "élément" dans ce cas signifie
soit un article, soit un module de front office ou soit un élément de contenu.
A la différence des trois autres hooks `getArticle`, `getFrontendModule` et
`getContentElement`, on peut prévenir la création du balisage complet. Le hook
passe le modèle de l'instance et l'état de visibilité courant en arguments et
attend le nouvel état de visibilité comme valeur de retour. Il est disponible à
partir de la version 3.2.RC1.

```php
// config.php
$GLOBALS['TL_HOOKS']['isVisibleElement'][] = array('MyClass', 'myIsVisibleElement');

// MyClass.php
public function myIsVisibleElement($objElement, $blnIsVisible)
{
    if ($objElement instanceof ContentElement)
    {
        // Vérifiez si cet élément de contenu peut être affiché
        if ($this->myElementCanBeShownInFrontend($objElement))
        {
            return true;
        }
    }

    // Sinon, nous ne voulons pas changer l'état de visibilité
    return $blnIsVisible;
}
```


### listComments

Le hook `listComments` est déclenché lorsque des commentaires sont listés dans
le back office. Il passe l'enregistrement courant en argument et attend une
chaîne de caractères comme valeur de retour. Il est disponible à partir de la
version 2.8.RC2.

```php
// config.php
$GLOBALS['TL_HOOKS']['listComments'][] = array('MyClass', 'myListComments');

// MyClass.php
public function myListComments($arrRow)
{
    return '<a href="contao/main.php?do= … ">' . $arrRow['title'] . '</a>';
}
```


### loadFormField

Le hook `loadFormField` est déclenché lorsqu'un champ de formulaire est chargé.
Il passe l'objet Widget, l'ID et les données du formulaire en arguments et
attend un objet Widget comme valeur de retour. Il est disponible à partir de
la version 2.5.0.

```php
// config.php
$GLOBALS['TL_HOOKS']['loadFormField'][] = array('MyClass', 'myLoadFormField');

// MyClass.php
public function myLoadFormField(Widget $objWidget, $strForm, $arrForm)
{
    $objWidget->class = 'myclass';
    return $objWidget;
}
```


### loadDataContainer

Le hook `loadDataContainer` est déclenché lorsqu'un fichier DCA est chargé. Il
passe le nom de fichier en argument et n'attend pas de valeur de retour. Il est
disponible à partir de la version 2.8.2.


```php
// config.php
$GLOBALS['TL_HOOKS']['loadDataContainer'][] = array('MyClass', 'myLoadDataContainer');

// MyClass.php
public function myLoadDataContainer($strName)
{
    // Faire quelque chose
}
```


### loadLanguageFile

Le hook `loadLanguageFile` est déclenché au chargement d'un fichier de langues.
Il passe le nom du fichier et la langue en arguments et n'attend pas de valeur
de retour. Il est disponible à partir de la version 2.8.RC1.

```php
// config.php
$GLOBALS['TL_HOOKS']['loadLanguageFile'][] = array('MyClass', 'myLoadLanguageFile');

// MyClass.php
public function myLoadLanguageFile($strName, $strLanguage)
{
    // Faire quelque chose
}
```


### outputBackendTemplate

Le hook `outputBackendTemplate` est déclenché lors de l'affichage à l'écran
d'un modèle du back office. Il passe le contenu et le nom du modèle en
arguments et attend le contenu du modèle comme valeur de retour. Il est
disponible à partir de la version 2.6.0.

```php
// config.php
$GLOBALS['TL_HOOKS']['outputBackendTemplate'][] = array('MyClass', 'myOutputBackendTemplate');

// MyClass.php
public function myOutputBackendTemplate($strContent, $strTemplate)
{
    if ($strTemplate == 'be_main')
    {
        // Modification de la sortie
    }

    return $strContent;
}
```


### outputFrontendTemplate

Le hook `outputFrontendTemplate` est déclenché lors de l'affichage à l'écran
d'un modèle du front office. Il passe le contenu et le nom du modèle en
arguments et attend le contenu du modèle comme valeur de retour. Il est
disponible à partir de la version 2.6.0.

```php
// config.php
$GLOBALS['TL_HOOKS']['outputFrontendTemplate'][] = array('MyClass', 'myOutputFrontendTemplate');

// MyClass.php
public function myOutputFrontendTemplate($strContent, $strTemplate)
{
    if ($strTemplate == 'fe_page')
    {
        // Modification de la sortie
    }

    return $strContent;
}
```


### parseBackendTemplate

Le hook `parseBackendTemplate` est déclenché lorsqu'un modèle de back office
est analysé ("parsé"). Il passe le contenu et le nom du modèle en arguments
et attend le contenu du modèle comme valeur de retour. Il est disponible à
partir de la version 2.6.0.

```php
// config.php
$GLOBALS['TL_HOOKS']['parseBackendTemplate'][] = array('MyClass', 'myParseBackendTemplate');

// MyClass.php
public function myParseBackendTemplate($strContent, $strTemplate)
{
    if ($strTemplate == 'be_main')
    {
        // Modification de la sortie
    }

    return $strContent;
}
```


### parseFrontendTemplate

Le hook `parseFrontendTemplate` est déclenché lors de l'analyse ("parsing")
d'un modèle de front office. Il passe le contenu et le nom du modèle en
arguments et attend le contenu du modèle comme valeur de retour. Il est
disponible à partir de la version 2.6.0.

```php
// config.php
$GLOBALS['TL_HOOKS']['parseFrontendTemplate'][] = array('MyClass', 'myParseFrontendTemplate');

// MyClass.php
public function myParseFrontendTemplate($strContent, $strTemplate)
{
    if ($strTemplate == 'ce_text')
    {
        // Modification de la sortie
    }

    return $strContent;
}
```


### parseTemplate

Le hook `parseTemplate` est déclenché avant le processus d'analyse d'un modèle.
Il reçoit une instance `Template` (qui peut être `FrontendTemplate` ou
`BackendTemplate`) en argument et n'attend pas de valeur de retour. Il est
disponible à partir de la version 2.10.0.

```php
// config.php
$GLOBALS['TL_HOOKS']['parseTemplate'][] = array('MyClass', 'myParseTemplate');

// MyClass.php
public function myParseTemplate($objTemplate)
{
    if ($objTemplate->getName() == 'mod_html')
    {
        // Modifier l'objet
    }
}
```


### postDownload

Le hook `postDownload` est déclenché après qu'un fichier ait été téléchargé
avec l'élément téléchargement(s). Il passe le nom du fichier en argument et
n'attend pas de valeur de retour. Il est disponible à partir de la version
2.4.6.

```php
// config.php
$GLOBALS['TL_HOOKS']['postDownload'][] = array('MyClass', 'myPostDownload');

// MyClass.php
public function myPostDownload($strFile)
{
    // Faire quelque chose
}
```


### postLogin

Le hook `postLogin` est déclenché après qu'un membre front office ou un
utilisateur back office se soit identifié. Il passe l'objet User en
argument et n'attend pas de valeur de retour.

```php
// config.php
$GLOBALS['TL_HOOKS']['postLogin'][] = array('MyClass', 'myPostLogin');

// MyClass.php
public function myPostLogin(User $objUser)
{
    // Faire quelque chose
}
```


### postLogout

Le hook `postLogout` est déclenché après qu'un membre front office ou un
utilisateur back office se soit déconnecté. Il passe l'objet User
en argument et n'attend pas de valeur de retour.

```php
// config.php
$GLOBALS['TL_HOOKS']['postLogout'][] = array('MyClass', 'myPostLogout');

// MyClass.php
public function myPostLogout(User $objUser)
{
    // Faire quelque chose
}
```


### postUpload

Le hook `postUpload` est déclenché après qu'un utilisateur ait envoyé un
ou plusieurs fichiers dans le back office. Il passe un tableau de noms de
fichiers en argument et n'attend pas de valeur de retour. Il est disponible
à partir de la version 2.6.4.

```php
// config.php
$GLOBALS['TL_HOOKS']['postUpload'][] = array('MyClass', 'myPostUpload');

// MyClass.php
public function myPostUpload($arrFiles)
{
    // Faire quelque chose
}
```


### prepareFormData

Le hook `prepareFormData` est déclenché après qu'un formulaire a été soumis.
Il passe le tableau des données, le tableau des labels et l'objet du formulaire
comme arguments et n'attend pas de valeur de retour. De cette façon, les données
peuvent être modifiées ou étendues, avant l'exécution des actions comme l'envoi
de messagerie ou le stockage de données. Il est disponible à partir de la
version 3.0.0.

```php
// config.php
$GLOBALS['TL_HOOKS']['prepareFormData'][] = array('MyClass', 'myPrepareFormData');

// MyClass.php
public function myPrepareFormData(&$arrSubmitted, $arrLabels, $objForm)
{
    // Faire quelque chose
}
```


### printArticleAsPdf

Le hook `printArticleAsPdf` est déclenché lorsqu'un article est exporté au
format PDF. Il passe le texte de l'article et l'objet Article en arguments
et n'attend pas de valeur de retour. Il est disponible à partir de la version
2.8.RC1.

```php
// config.php
$GLOBALS['TL_HOOKS']['printArticleAsPdf'][] = array('MyClass', 'myPrintArticleAsPdf');

// MyClass.php
public function myPrintArticleAsPdf($strArticle, Database_Result $objArticle)
{
    // Faire quelque chose
    exit;
}
```


### processFormData

Le hook `processFormData` est déclenché après la soumission d'un formulaire.
Il passe le tableau des données du formulaire, le [tableau conteneur de données][2]
et le tableau de fichiers en arguments et n'attend pas de valeur de retour.
Il est disponible à partir de la version 2.4.4.

```php
// config.php
$GLOBALS['TL_HOOKS']['processFormData'][] = array('MyClass', 'myProcessFormData');

// MyClass.php
public function myProcessFormData($arrPost, $arrForm, $arrFiles)
{
    // Faire quelque chose
}
```


### removeOldFeeds

Le hook `removeOldFeeds` est déclenché lors de la suppression des vieux fichiers
XML du répertoire de Contao. Il ne passe pas d'arguments et attend un tableau de
noms de fichiers à conserver comme valeur de retour. Il est disponible à partir
de la version 2.5.8.

```php
// config.php
$GLOBALS['TL_HOOKS']['removeOldFeeds'][] = array('MyClass', 'myRemoveOldFeeds');

// MyClass.php
public function myRemoveOldFeeds()
{
    return array('custom.xml');
}
```


### removeRecipient

Le hook `removeRecipient` est déclenché à la suppression d'un destinataire de
newsletter. Il passe l'adresse e-mail et les ID de la liste de diffusion en
arguments et n'attend pas de valeur de retour. Il est disponible à partir de
la version 2.8.RC1.

```php
// config.php
$GLOBALS['TL_HOOKS']['removeRecipient'][] = array('MyClass', 'myRemoveRecipient');

// MyClass.php
public function myRemoveRecipient($strEmail, $arrChannels)
{
    // Faire quelque chose
}
```


### replaceInsertTags

Le hook `replaceInsertTags` est déclenché lorsqu'une balise d'insertion
inconnue est trouvée. Il passe la balise d'insertion en argument et attend la
valeur de remplacement ou `false` comme valeur de retour. Il est disponible
à partir de la version 2.6.0.

```php
// config.php
$GLOBALS['TL_HOOKS']['replaceInsertTags'][] = array('MyClass', 'myReplaceInsertTags');

// MyClass.php
public function myReplaceInsertTags($strTag)
{
    if ($strTag == 'mytag')
    {
        return 'mytag replacement';
    }

    return false;
}
```


### reviseTable

Le hook `reviseTable` est déclenché lorsque Contao supprime d'une table des
enregistrements orphelins. Il passe le nom de la table courante, les ID de
tous les nouveaux enregistrements, le nom de la table parente, et les noms
de toutes les tables enfants en arguments et attend un booléen comme valeur
de retour (le retour de la valeur `true` provoque le rechargement de la page
courante). Il est disponible à partir de la version 2.6.4.

```php
// config.php
$GLOBALS['TL_HOOKS']['reviseTable'][] = array('MyClass', 'myReviseTable');

// MyClass.php
public function myReviseTable($table, $new_records, $parent_table, $child_tables)
{
    // Faire quelque chose
}
```


### setNewPassword

Le hook `setNewPassword` est déclenché après la saisie d'un nouveau mot de
passe. Il passe l'objet User et le mot de passe crypté en arguments
et n'attend pas de valeur de retour. Il est disponible à partir de la
version 2.2.3.

```php
// config.php
$GLOBALS['TL_HOOKS']['setNewPassword'][] = array('MyClass', 'mySetNewPassword');

// MyClass.php
public function mySetNewPassword($objUser, $strPassword)
{
    // Faire quelque chose
}
```


### validateFormField

Le hook `validateFormField` est déclenché à la soumission d'un champ de
formulaire. Il passe l'objet Widget et l'ID du formulaire en arguments et
attend un objet Widget comme valeur de retour. Il est disponible à partir de
la version 2.5.0.

```php
// config.php
$GLOBALS['TL_HOOKS']['validateFormField'][] = array('MyClass', 'myValidateFormField');

// MyClass.php
public function myValidateFormField(Widget $objWidget, $intId)
{
    if ($objWidget instanceof FormPassword)
    {
        // Faire quelque chose
    }

    return $objWidget;
}
```


[1]: ../06-tableaux-conteneurs-de-donnees/callbacks.md#callbacks
[2]: ../06-tableaux-conteneurs-de-donnees/README.md
