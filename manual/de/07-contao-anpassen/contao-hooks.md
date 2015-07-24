## Contao-Hooks

Hooks funktionieren ähnlich wie die [Callback-Funktionen][1] des Data Container
Arrays. Sie können eine oder mehrere Funktionen für ein bestimmtes Ereignis
registrieren, die dann bei dessen Eintreten ausgeführt werden. Dadurch lässt
sich der Core um eigene Funktionalität erweitern.


### activateAccount

Der "activateAccount"-Hook wird bei der Aktivierung eines neuen Mitgliederkontos
ausgeführt. Er übergibt das Benutzer-Objekt als Argument und erwartet keinen
Rückgabewert. Hinzugefügt in Version 2.4.3.

```php
// config.php
$GLOBALS['TL_HOOKS']['activateAccount'][] = array('MyClass', 'myActivateAccount');

// MyClass.php
public function myActivateAccount(Database_Result $objUser)
{
    // Beliebiger Code
}
```


### activateRecipient

Der "activateRecipient"-Hook wird bei der Aktivierung eines neuen
Newsletter-Abonnenten ausgeführt. Er übergibt die E-Mail-Adresse, die IDs der
Empfänger und die IDs der Verteiler als Argument und erwartet keinen
Rückgabewert. Hinzugefügt in Version 2.8.RC1.

```php
// config.php
$GLOBALS['TL_HOOKS']['activateRecipient'][] = array('MyClass', 'myActivateRecipient');

// MyClass.php
public function myActivateRecipient($strEmail, $arrRecipients, $arrChannels)
{
    // Beliebiger Code
}
```


### addComment

Der "addComment"-Hook wird beim Hinzufügen eines Kommentars ausgeführt. Er
übergibt die ID des Datensatzes und das Datenarray als Argument und erwartet
keinen Rückgabewert. Hinzugefügt in Version 2.8.2.

```php
// config.php
$GLOBALS['TL_HOOKS']['addComment'][] = array('MyClass', 'myAddComment');

// MyClass.php
public function myAddComment($intId, $arrSet)
{
    // Beliebiger Code
}
```


### addCustomRegexp

Der "addCustomRegexp"-Hook wird beim Antreffen eines unbekannten regulären
Ausdrucks ausgeführt. Er übergibt den Namen des Ausdrucks, den aktuellen Wert
und das Widget-Objekt als Argument und erwartet einen booleschen Rückgabewert.
Hinzugefügt in Version 2.6.2.

```php
// config.php
$GLOBALS['TL_HOOKS']['addCustomRegexp'][] = array('MyClass', 'myAddCustomRegexp');

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

Der "addLogEntry"-Hook wird beim Anlegen eines Log-Eintrags ausgeführt. Er
übergibt den Log-Text, die Funktion und die Aktion als Argument und erwartet
keinen Rückgabewert. Hinzugefügt in Version 2.8.RC1.

```php
// config.php
$GLOBALS['TL_HOOKS']['addLogEntry'][] = array('MyClass', 'myAddLogEntry');

// MyClass.php
public function myAddLogEntry($strText, $strFunction, $strAction)
{
    // Beliebiger Code
}
```


### checkCredentials

Der "checkCredentials"-Hook wird bei der Eingabe eines falschen Passworts bei der
Anmeldung ausgeführt. Er übergibt den Benutzernamen und das Passwort sowie das
Benutzer-Objekt als Argument und erwartet einen booleschen Rückgabewert.
Hinzugefügt in Version 2.6.0.

```php
// config.php
$GLOBALS['TL_HOOKS']['checkCredentials'][] = array('MyClass', 'myCheckCredentials');

// MyClass.php
public function myCheckCredentials($strUsername, $strPassword, User $objUser)
{
    // Eine globale Datenbank abfragen
    if ($this->checkGlobalDbFor($strUsername, $strPassword))
    {
        return true;
    }

    return false;
}
```


### closeAccount

Der "closeAccount"-Hook wird bei der Schließung eines Benutzerkontos
ausgeführt. Er übergibt die ID des Benutzers, den Betriebsmodus und das
Modul-Objekt als Argument und erwartet keinen Rückgabewert. Hinzugefügt in
Version 2.8.0.

```php
// config.php
$GLOBALS['TL_HOOKS']['closeAccount'][] = array('MyClass', 'myCloseAccount');

// MyClass.php
public function myCloseAccount($intId, $strMode, $objModule)
{
    if ($strMode == 'close_delete')
    {
        // Beliebiger Code
    }
}
```


### colorizeLogEntries

Der "colorizeLogEntries"-Hook wird im Label-Callback eines tl_log-Eintrags ausgeführt.
Er übergibt den Log-Eintrag als Array und das Label als String und erwartet einen
HTML-String als Rückgabewert. Dieser Hook kann dafür genutzt werden, ein Label
für eigene Log-Kategorien zu generieren oder bestehende Labels zu modifizieren.
Hinzugefügt in Version 3.3.RC1.


```php
// config.php
$GLOBALS['TL_HOOKS']['colorizeLogEntries'][] = array('MyClass', 'colorizeLogEntries');

// MyClass.php
public function colorizeLogEntries($row, $label)
{
    // Beliebiger Code

    return $label;
}
```


### compileDefinition

Der "compileDefinition"-Hook wird bei der Erstellung einer Formatdefinition in
einem Stylesheet ausgeführt. Er übergibt das Konfigurationsarray als Argument
und erwartet einen String als Rückgabewert. Hinzugefügt in Version 2.9.4.

```php
// config.php
$GLOBALS['TL_HOOKS']['compileDefinition'][] = array('MyClass', 'myCompileDefinition');

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

Der "compileFormFields"-Hook wird vor der Ausgabe eines Formulars ausgeführt.
Er übergibt ein Array mit FormFieldModel-Objekten, die Form-Id und das Formular-Objekt als
Argument und erwartet das Array mit FormFieldModel-Objekten als Rückgabewert. Hier können
Formularfelder dynamisch angepasst werden, bevor sie ausgegeben werden.
Hinzugefügt in Version 3.2.

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
    if ($objFields->name == 'my_form_field_1')
    {
      // Beliebiger Code
          }
  }
    }

    return $arrFields;
}
```


### createDefinition

Der "createDefinition"-Hook wird beim Import einer Formatdefinition eines
Stylesheets ausgeführt. Er übergibt Schlüssel und Wert, die originale
Formatdefinition sowie das Daten-Array als Argument und erwartet ein Array oder
`false` als Rückgabewert. Hinzugefügt in Version 2.9.4.

```php
// config.php
$GLOBALS['TL_HOOKS']['createDefinition'][] = array('MyClass', 'myCreateDefinition');

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

Der "createNewUser"-Hook wird bei der Registrierung eines neuen Mitglieds
ausgeführt. Er übergibt die ID des neuen Benutzers und das Datenarray als
Argument und erwartet keinen Rückgabewert. Hinzugefügt in Version 2.2.0.

```php
// config.php
$GLOBALS['TL_HOOKS']['createNewUser'][] = array('MyClass', 'myCreateNewUser');

// MyClass.php
public function myCreateNewUser($intId, $arrData)
{
    // Den Datensatz modifizieren
}
```


### executePreActions

Der "executePreActions"-Hook wird bei unbekannten Ajax-Anfragen ausgeführt, die
keine DCA-Objekt benötigen. Er übergibt den Namen der Aktion als Argument und
erwartet keinen Rückgabewert. Hinzugefügt in Version 2.6.1.

```php
// config.php
$GLOBALS['TL_HOOKS']['executePreActions'][] = array('MyClass', 'myExecutePreActions');

// MyClass.php
public function myExecutePreActions($strAction)
{
    if ($strAction == 'update')
    {
        // Beliebiger Code
    }
}
```


### executePostActions

Der "executePostActions"-Hook wird bei unbekannten Ajax-Anfragen ausgegeben, die
ein DCA-Objekt benötigen. Er übergibt den Namen der Aktion und das
DataContainer-Objekt als Argument und erwartet keinen Rückgabewert. Hinzugefügt
in Version 2.6.1.

```php
// config.php
$GLOBALS['TL_HOOKS']['executePostActions'][] = array('MyClass', 'myExecutePostActions');

// MyClass.php
public function myExecutePostActions($strAction, DataContainer $dc)
{
    if ($strAction == 'update')
    {
        // Beliebiger Code
    }
}
```


### generateBreadcrumb

Der "generateBreadcrumb"-Hook ermöglicht das Modifizieren der Pfadnavigation.
Er übergibt das Navigations-Array und das Modul-Objekt als Argument und erwartet
ein Array als Rückgabewert. Hinzugefügt in Version 2.10.0

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

Der "generateFrontendUrl"-Hook wird bei der Erstellung einer Frontend-URL
ausgeführt. Er übergibt die originale URL als Argument und erwartet eine
Zeichenkette als Rückgabewert. Hinzugefügt in Version 2.5.8.

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

Der "generatePage"-Hook wird vor der Erstellung des Seitenlayouts ausgeführt.
Er übergibt das Seitenobjekt, das Layoutobjekt und eine Eigenreferenz als
Argument und erwartet keinen Rückgabewert. Hinzugefügt in Version 2.8.RC1.

```php
// config.php
$GLOBALS['TL_HOOKS']['generatePage'][] = array('MyClass', 'myGeneratePage');

// MyClass.php
public function myGeneratePage(\PageModel $objPage, \LayoutModel $objLayout, \PageRegular $objPageRegular)
{
    // Beliebiger Code
}
```


### getAllEvents

Der "getAllEvents"-Hook ermöglicht das Modifizieren von Terminen in Kalendern
und Eventmodulen. Er übergibt das originale Datenarray, die IDs der
Elternelemente sowie die Start- und Endzeit als Argument und erwartet ein
Datenarray als Rückgabewert. Hinzugefügt in Version 2.6.4.

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


### getAttributesFromDca

Der "getAttributesFromDca"-Hook ermöglicht das Modifizieren der Formularfeldattribute.
Er übergibt die originalen Attribute als Array und das DataContainer-Objekt und erwartet
ein Array von Attributen als Rückgabewert. Hinzugefügt in Version 3.2.RC1.

```php
// config.php
$GLOBALS['TL_HOOKS']['getAttributesFromDca'][] = array('MyClass', 'myGetAttributesFromDca');

// MyClass.php
public function myGetAttributesFromDca($arrAttributes, $objDca)
{
    // do something
    return $arrAttributes;
}
```


### getContentElement

Der "getContentElement"-Hook wird beim Rendern von Inhaltselementen ausgeführt.
Er übergibt das Datenbankobjekt und den Ausgabe-String als Argument und
erwartet einen Ausgabe-String als Rückgabewert. Hinzugefügt in Version 2.9.0.

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

Der "getImage"-Hook wird bei der Erstellung eines Vorschaubildes ausgeführt und
ermöglicht das Hinzufügen einer eigenen Routine. Er übergibt den Pfad, die
Breite und Höhe, den Modus, den Cache-Namen und das Dateiobjekt als Argument
und erwartet einen Pfad als Rückgabewert. Hinzugefügt in Version 2.8.RC1.

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

Der "getPageIdFromUrl"-Hook wird beim Auswerten der URL-Fragmente ausgeführt.
Er übergibt das Fragment-Array als Argument und erwartet ein Datenarray als
Rückgabewert. Hinzugefügt in Version 2.5.4.

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

Der "getPageLayout"-Hook wird vor dem Initialisieren des Frontend-Templates
ausgeführt. Er übergibt das Seitenobjekt, das Layoutobjekt und eine
Eigenreferenz als Argument und erwartet keinen Rückgabewert. Hinzugefügt in
Version 3.1.0.

```php
// config.php
$GLOBALS['TL_HOOKS']['getPageLayout'][] = array('MyClass', 'mygetPageLayout');

// MyClass.php
public function mygetPageLayout(\PageModel $objPage, \LayoutModel $objLayout, \PageRegular $objPageRegular)
{
    // Beliebiger Code
}
```


### getSearchablePages

Der "getSearchablePages"-Hook wird beim Aufbau des Suchindex ausgeführt. Er
übergibt das URL-Array und die ID der Wurzelseite als Argument und erwartet ein
Array mit absoluten URLs (!) als Rückgabewert. Hinzugefügt in Version 2.2.0.

```php
// config.php
$GLOBALS['TL_HOOKS']['getSearchablePages'][] = array('MyClass', 'myGetSearchablePages');

// MyClass.php
public function myGetSearchablePages($arrPages, $intRoot)
{
    return array_merge($arrPages, array('Additional pages'));
}
```

### getSystemMessages

Der "getSystemMessages"-Hook erlaubt zusätzliche Informationen auf der "Welcome-Page" anzuzeigen. Es werden keine Parameter benötigt. Als Rückgabewert wird der Text inkl. HTML angegeben. Hinzugefügt in Version 2.11.0

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['getSystemMessages'][] = array('MyClass', 'myGetSystemMessages');

// MyClass.php
public function myGetSystemMessages()
{
    $this->import('BackendUser', 'User');

    // Display a warning if the system admin's email is not set
    if ($GLOBALS['TL_ADMIN_EMAIL'] == '')
    {
        return '<p class="tl_error">Please add your email address to system settings.';
    }

    return '';
}
```

### initializeSystem

Der "initializeSystem"-Hook wird bei der Initialisierung des Systems ausgeführt.
Hinzugefügt in Version 3.1.RC1.

```php
// config.php
$GLOBALS['TL_HOOKS']['initializeSystem'][] = array('MyClass', 'myInitializeSystem');

// MyClass.php
public function myInitializeSystem()
{
    // Beliebiger Code
}
```


### importUser

Der "importUser"-Hook wird beim Antreffen eines unbekannten Benutzernamens
ausgeführt. Er übergibt den Benutzernamen, das Passwort und den Tabellennamen
als Argument und erwartet einen booleschen Rückgabewert. Hinzugefügt in Version
2.7.RC1.

```php
// config.php
$GLOBALS['TL_HOOKS']['importUser'][] = array('MyClass', 'myImportUser');

// MyClass.php
public function myImportUser($strUsername, $strPassword, $strTable)
{
    if ($strTable == 'tl_member')
    {
        // Benutzer von einem LDAP-Server importieren
        if ($this->importUserFromLdap($strUsername, $strPassword))
        {
            return true;
        }
    }

    return false;
}
```


### isVisibleElement

Der "isVisibleElement"-Hook wird beim Überprüfen, ob ein Element im Frontend sichtbar
sein soll oder nicht, ausgeführt. Ein "Element" bedeutet an dieser Stelle entweder ein
Artikel, ein Frontend-Modul oder ein Inhaltselement. Im Gegensatz zu den drei anderen
Hooks "getArticle", "getFrontendModule" und "getContentElement" kann hier das Generieren
des gesamten Markups verhindert werden. Der Hook übergibt das Model des Elements sowie
den aktuellen Sichtbarkeitsstatus als Argumente und erwartet den neuen Sichtbarkeitsstatus
als Rückgabewert. Hinzugefügt in Version 3.2.RC1.

```php
// config.php
$GLOBALS['TL_HOOKS']['isVisibleElement'][] = array('MyClass', 'myIsVisibleElement');

// MyClass.php
public function myIsVisibleElement($objElement, $blnIsVisible)
{
    if ($objElement instanceof ContentElement)
    {
        // Prüfen ob das Inhaltselement angezeigt werden darf
        if ($this->myElementCanBeShownInFrontend($objElement))
        {
            return true;
        }
    }

    // Andernfalls verändern wir den Sichtbarkeitsstatus nicht
    return $blnIsVisible;
}
```


### listComments

Der "listComments"-Hook wird bei der Darstellung von Kommentaren im Backend
ausgeführt. Er übergibt den aktuellen Datensatz als Argument und erwartet
einen String als Rückgabewert. Hinzugefügt in Version 2.8.RC2.

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

Der "loadFormField"-Hook wird beim Laden eines Formularfeldes ausgeführt. Er
übergibt das Widget-Objekt, die ID und die Metadaten des Formulars als Argument
und erwartet ein Widget-Objekt als Rückgabewert. Hinzugefügt in Version 2.5.0.

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

Der "loadDataContainer"-Hook wird beim Laden eines Data Containers ausgeführt.
Er übergibt den Namen der DCA-Datei als Argument und erwartet keinen
Rückgabewert. Hinzugefügt in Version 2.8.2.

```php
// config.php
$GLOBALS['TL_HOOKS']['loadDataContainer'][] = array('MyClass', 'myLoadDataContainer');

// MyClass.php
public function myLoadDataContainer($strName)
{
    // Beliebiger Code
}
```


### loadLanguageFile

Der "loadLanguageFile"-Hook wird beim Laden einer Sprachdatei ausgeführt. Er
übergibt den Namen der Sprachdatei und die Sprache als Argument und erwartet
keinen Rückgabewert. Hinzugefügt in Version 2.8.RC1.

```php
// config.php
$GLOBALS['TL_HOOKS']['loadLanguageFile'][] = array('MyClass',
'myLoadLanguageFile');

// MyClass.php
public function myLoadLanguageFile($strName, $strLanguage)
{
    // Beliebiger Code
}
```


### outputBackendTemplate

Der "outputBackendTemplate"-Hook wird bei der Ausgabe eines Backend-Templates
auf dem Bildschirm ausgeführt. Er übergibt Inhalt und Name des Templates als
Argument und erwartet den geänderten Template-Inhalt als Rückgabewert.
Hinzugefügt in Version 2.6.0.

```php
// config.php
$GLOBALS['TL_HOOKS']['outputBackendTemplate'][] = array('MyClass', 'myOutputBackendTemplate');

// MyClass.php
public function myOutputBackendTemplate($strContent, $strTemplate)
{
    if ($strTemplate == 'be_main')
    {
        // Ausgabe modifizieren
    }

    return $strContent;
}
```


### outputFrontendTemplate

Der "outputFrontendTemplate"-Hook wird bei der Ausgabe eines Frontend-Templates
auf dem Bildschirm ausgeführt. Er übergibt Inhalt und Name des Templates als
Argument und erwartet den geänderten Template-Inhalt als Rückgabewert.
Hinzugefügt in Version 2.6.0.

```php
// config.php
$GLOBALS['TL_HOOKS']['outputFrontendTemplate'][] = array('MyClass', 'myOutputFrontendTemplate');

// MyClass.php
public function myOutputFrontendTemplate($strContent, $strTemplate)
{
    if ($strTemplate == 'fe_page')
    {
        // Ausgabe modifizieren
    }

    return $strContent;
}
```


### parseBackendTemplate

Der "parseBackendTemplate"-Hook wird bei der Aufbereitung eines
Backend-Templates ausgeführt. Er übergibt Inhalt und Name des Templates als
Argument und erwartet den geänderten Template-Inhalt als Rückgabewert.
Hinzugefügt in Version 2.6.0.

```php
// config.php
$GLOBALS['TL_HOOKS']['parseBackendTemplate'][] = array('MyClass', 'myParseBackendTemplate');

// MyClass.php
public function myParseBackendTemplate($strContent, $strTemplate)
{
    if ($strTemplate == 'be_main')
    {
        // Ausgabe modifizieren
    }

    return $strContent;
}
```


### parseFrontendTemplate

Der "parseFrontendTemplate"-Hook wird bei der Aufbereitung eines
Frontend-Templates ausgeführt. Er übergibt Inhalt und Name des Templates als
Argument und erwartet den geänderten Template-Inhalt als Rückgabewert.
Hinzugefügt in Version 2.6.0.

```php
// config.php
$GLOBALS['TL_HOOKS']['parseFrontendTemplate'][] = array('MyClass', 'myParseFrontendTemplate');

// MyClass.php
public function myParseFrontendTemplate($strContent, $strTemplate)
{
    if ($strTemplate == 'ce_text')
    {
        // Ausgabe modifizieren
    }

    return $strContent;
}
```

### parseTemplate

Der "parseTemplate"-Hook wird vor der Verarbeitung eines Templates ausgeführt.
Er übergibt die `Template`-Instanz als Argument (kann `FrontendTemplate` und
`BackendTemplate` sein) und erwartet keinen Rückgabewert.
Hinzugefügt in Version 2.10.0.

```php
// config.php
$GLOBALS['TL_HOOKS']['parseTemplate'][] = array('MyClass', 'myParseTemplate');

// MyClass.php
public function myParseTemplate($objTemplate)
{
    if ($objTemplate->getName() == 'mod_html')
    {
        // Objekt modifizieren
    }
}
```

### postDownload

Der "postDownload"-Hook wird nach dem Herunterladen einer Datei mit Hilfe des
Download(s)-Elements ausgeführt. Er übergibt den Dateinamen als Argument und
erwartet keinen Rückgabewert. Hinzugefügt in Version 2.4.6.

```php
// config.php
$GLOBALS['TL_HOOKS']['postDownload'][] = array('MyClass', 'myPostDownload');

// MyClass.php
public function myPostDownload($strFile)
{
    // Beliebiger Code
}
```


### postLogin

Der "postLogin"-Hook wird nach der Anmeldung eines Frontend-Mitglieds oder
Backend-Benutzers ausgeführt. Er übergibt das Benutzerobjekt als Argument
und erwartet keinen Rückgabewert.

```php
// config.php
$GLOBALS['TL_HOOKS']['postLogin'][] = array('MyClass', 'myPostLogin');

// MyClass.php
public function myPostLogin(User $objUser)
{
    // Beliebiger Code
}
```


### postLogout

Der "postLogout"-Hook wird nach der Abmeldung eines Frontend-Mitglieds oder
Backend-Benutzers ausgeführt. Er übergibt das Benutzerobjekt als Argument
und erwartet keinen Rückgabewert.

```php
// config.php
$GLOBALS['TL_HOOKS']['postLogout'][] = array('MyClass', 'myPostLogout');

// MyClass.php
public function myPostLogout(User $objUser)
{
    // Beliebiger Code
}
```


### postUpload

Der "postUpload"-Hook wird nach dem Hochladen einer oder mehrerer Dateien in der
Contao-Dateiverwaltung ausgeführt. Er übergibt ein Array mit Dateinamen als
Argument und erwartet keinen Rückgabewert. Hinzugefügt in Version 2.6.4.

```php
// config.php
$GLOBALS['TL_HOOKS']['postUpload'][] = array('MyClass', 'myPostUpload');

// MyClass.php
public function myPostUpload($arrFiles)
{
    // Beliebiger Code
}
```


### prepareFormData

Der `prepareFormData`-Hook wird beim Absenden eines Formulars ausgeführt.
Er übergibt die Formulardaten, die Feldbezeichnungen und das Formular-Objekt.
Damit lassen sich die Daten ändern oder erweitern, bevor Aktionen wie
z.B. E-Mail Versand oder in der Datenbank speichern ausgeführt wird.
Hinzugefügt in Version 3.0.0.

```php
// config.php
$GLOBALS['TL_HOOKS']['prepareFormData'][] = array('MyClass', 'myPrepareFormData');

// MyClass.php
public function myPrepareFormData(&$arrSubmitted, $arrLabels, $objForm)
{
    // Beliebiger Code
}
```


### printArticleAsPdf

Der "printArticleAsPdf"-Hook wird bei der Ausgabe eines Artikels im PDF-Format
ausgeführt. Er übergibt den Artikeltext und das Artikelobjekt als Argument
und erwartet keinen Rückgabewert. Hinzugefügt in Version 2.8.RC1.

```php
// config.php
$GLOBALS['TL_HOOKS']['printArticleAsPdf'][] = array('MyClass', 'myPrintArticleAsPdf');

// MyClass.php
public function myPrintArticleAsPdf($strArticle, Database_Result $objArticle)
{
    // Beliebiger Code
    exit;
}
```


### processFormData

Der "processFormData"-Hook wird nach dem Abschicken eines Formulars ausgeführt.
Er übergibt das Datenarray, das [Data Container Array][2] und das Dateiarray
als Argument und erwartet keinen Rückgabewert. Hinzugefügt in Version 2.4.4.

```php
// config.php
$GLOBALS['TL_HOOKS']['processFormData'][] = array('MyClass', 'myProcessFormData');

// MyClass.php
public function myProcessFormData($arrPost, $arrForm, $arrFiles)
{
    // Beliebiger Code
}
```


### removeOldFeeds

Der "removeOldFeeds"-Hook wird beim Entfernen alter XML-Dateien aus dem
Contao-Verzeichnis ausgeführt. Er übergibt nichts als Argument und erwartet
ein Array mit zu erhaltenden Dateien als Rückgabewert. Hinzugefügt in Version
2.5.8.

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

Der "removeRecipient"-Hook wird bei der Kündigung eines Newsletter-Abonnements
(Unsubscribe) ausgeführt. Er übergibt die E-Mail-Adresse und die IDs der
Verteiler als Argument und erwartet keinen Rückgabewert. Hinzugefügt in
Version 2.8.RC1.

```php
// config.php
$GLOBALS['TL_HOOKS']['removeRecipient'][] = array('MyClass', 'myRemoveRecipient');

// MyClass.php
public function myRemoveRecipient($strEmail, $arrChannels)
{
    // Beliebiger Code
}
```


### replaceInsertTags

Der "replaceInsertTags"-Hook wird beim Antreffen eines unbekannten Insert-Tags
ausgeführt. Er übergibt das Insert-Tag als Argument und erwartet die Ersetzung
oder `false` als Rückgabewert. Hinzugefügt in Version 2.6.0.

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

Der "reviseTable"-Hook wird beim Bereinigen verwaister Datensätze einer Tabelle
ausgeführt. Er übergibt den Namen der Tabelle, die IDs aller neu angelegten
Datensätze, den Namen der Elterntabelle und die Namen aller Kindtabellen als
Argument und erwartet einen booleschen Rückgabewert. Geben Sie `true` zurück,
um die Seite neu zu laden. Hinzugefügt in Version 2.6.4.

```php
// config.php
$GLOBALS['TL_HOOKS']['reviseTable'][] = array('MyClass', 'myReviseTable');

// MyClass.php
public function myReviseTable($table, $new_records, $parent_table, $child_tables)
{
    // Beliebiger Code
}
```


### setNewPassword

Der "setNewPassword"-Hook wird nach dem Abspeichern eines neuen Passworts
ausgeführt. Er übergibt das Benutzerobjekt und das verschlüsselte Passwort
als Argument und erwartet keinen Rückgabewert. Hinzugefügt in Version 2.2.3.

```php
// config.php
$GLOBALS['TL_HOOKS']['setNewPassword'][] = array('MyClass', 'mySetNewPassword');

// MyClass.php
public function mySetNewPassword($objUser, $strPassword)
{
    // Beliebiger Code
}
```


### validateFormField

Der "validateFormField"-Hook wird beim Abschicken eines Formularfeldes
ausgeführt. Er übergibt das Widget-Objekt und die ID des Formulars als
Argument und erwartet ein Widget-Objekt als Rückgabewert. Hinzugefügt in
Version 2.5.0.

```php
// config.php
$GLOBALS['TL_HOOKS']['validateFormField'][] = array('MyClass', 'myValidateFormField');

// MyClass.php
public function myValidateFormField(Widget $objWidget, $intId)
{
    if ($objWidget instanceof FormPassword)
    {
        // Beliebiger Code
    }

    return $objWidget;
}
```


[1]: ../06-data-container-arrays/callbacks.md#callbacks
[2]: ../06-data-container-arrays/README.md
