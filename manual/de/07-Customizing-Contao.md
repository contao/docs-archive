# Contao anpassen

Anpassbarkeit ist eine zentrale Anforderung an jede Applikation und besonders an
ein Content Management System. Contao bietet sehr viele Möglichkeiten, die
Konfiguration zu modifizieren, Felder und Bezeichnungen anzupassen, eigene
Routinen hinzuzufügen oder eigene Module zu erstellen. Sie können fast jeden
Ablauf der Contao Core-Engine beeinflussen, ohne dabei deren Dateien ändern zu
müssen.


##Internen Cache umgehen 

Vor der Anpassung von Contao oder der Entwicklung von Erweiterungen sollte 
unbedingt der interne Cache deaktiviert bzw. umgangen werden.
Dazu navigieren Sie im Backend zu "System"->"Einstellungen" und setzten einen 
Haken unter "Globale Einstellungen" bei "Internen Cache umgehen".

![](https://raw.github.com/contao/docs/3.1/manual/de/images/internen-cache-umgehen.jpg)

Sobald die Seite jedoch in den produktiven Betrieb geht, sollte unbedingt der 
Haken bei "Internen Cache umgehen" entfernt werden, da das System ohne den 
Cache gerade bei größeren Projekten um einiges langsamer reagiert.


## Konfiguration anpassen

Die Contao-Konfiguration ist in drei Bestandteile aufgeteilt: die
Systemkonfiguration, die DCA-Konfiguration und die Sprachkonfiguration. Das
globale Konfigurationsarray wird zur Laufzeit aus denjenigen Bestandteilen
zusammengesetzt, die für die Ausgabe einer Seiten gebraucht werden. Um Zeit und
Arbeitsspeicher zu sparen, werden nicht benötigte Konfigurationsdateien dabei
übersprungen.


### Die Systemkonfiguration anpassen

Die Systemkonfiguration ist in den `config.php`-Dateien der verschiedenen
Contao-Module gespeichert. Änderungen können updatesicher in der Datei
`system/config/localconfig.php` hinterlegt werden. Die meisten Parameter werden
in den Backend-Einstellungen gesetzt und automatisch in die lokale
Konfigurationsdatei geschrieben, so dass Sie diese in der Regel nicht manuell
bearbeiten müssen.

``` {.php}
// Den Extension Creator abschalten
unset($GLOBALS['BE_MOD']['devtools']['extension']);

### INSTALL SCRIPT START ###
$GLOBALS['TL_CONFIG']['debugMode'] = false;
$GLOBALS['TL_CONFIG']['displayErrors'] = false;
```

Platzieren Sie Ihre Änderungen unbedingt oberhalb der Zeile `INSTALL SCRIPT
START`, da sie andernfalls automatisch entfernt werden. Und **speichern Sie Ihre
Einstellungen niemals in der Datei config.php**, da diese Datei bei
Aktualisierungen überschrieben werden kann!


### Die DCA-Konfiguration anpassen

Contao verwendet [Data Container Arrays][1] zur Speicherung von
Tabellen-Metadaten. Die Data Container-Konfiguration ist in den `dca`-Ordnern
der verschiedenen Contao-Module hinterlegt und kann in der Datei
`system/config/dcaconfig.php` updatesicher angepasst werden.

``` {.php}
// Firma zu einem Pflichtfeld in der Mitgliedertabelle machen
$GLOBALS['TL_DCA']['tl_member']['fields']['company']['eval']['mandatory'] =
true;

// Firmennamen dürfen nur alphanumerische Zeichen beinhalten
$GLOBALS['TL_DCA']['tl_member']['fields']['company']['eval']['rgxp'] = 'alnum';

// Nur Administratoren dürfen Include-Elemente verwenden
if (!BackendUser::getInstance()->isAdmin)
{
    unset($GLOBALS['TL_CTE']['includes']);
}
```

Wie Sie sehen, eignet sich die Datei `dcaconfig.php` hervorragend für kleinere
Anpassung der Contao-Konfiguration. Größere Änderungen sollten jedoch zur
besseren Übersicht in einem eigenen Modul gekapselt werden.


### Bezeichnungen und Übersetzungen anpassen

Bezeichnungen und Übersetzungen sind in den `languages`-Ordnern der
verschiedenen Contao-Module hinterlegt. Jede Sprache wird anhand ihres
[ISO-639-1 Sprachcodes][2] identifiziert. Änderungen können updatesicher in
der Datei `system/config/langconfig.php` gespeichert werden.

``` {.php}
// Eine Bezeichnung in allen Sprachen ändern
$GLOBALS['TL_LANG']['MSC']['goBack'] = '«';

// Eine Bezeichnung in einer bestimmten Sprache ändern
if ($GLOBALS['TL_LANGUAGE'] == 'de')
{
    $GLOBALS['TL_LANG']['tl_layout']['column'] = 'Bereich';
}
elseif ($GLOBALS['TL_LANGUAGE'] == 'fr')
{
    $GLOBALS['TL_LANG']['tl_layout']['column'] = 'Section';
}
```

Auch Sprachanpassungen können in einem eigenen Modul gekapselt werden, was ab
einer bestimmten Anzahl empfohlen ist.


## Eigene Felder hinzufügen

Nehmen wir an, Sie möchten die Mitgliedertabelle um eine Kundennummer
erweitern. Da das Hinzufügen eines Feldes mehr erfordert als nur das Ändern
einer einzelnen Datei, wird das Anlegen eines eigenen Moduls im Verzeichnis
`system/modules` empfohlen. Denken Sie daran, dass Module in alphabetischer
Reihenfolge geladen werden. Nennen Sie es also nicht `custom`, wenn Sie damit
die `news`-Erweiterung anpassen wollen.


### Die DCA-Konfiguration erweitern

Legen Sie die Datei `dca/tl_member.php` in Ihrem Modulordner an und fügen Sie
die Metadaten des neuen Feldes ein.
Seit Contao 3 werden außerdem auch die dazugehörigen Felder sowie deren 
Konfiguration für die Datenbank unter `sql` direkt mit angegeben. 

``` {.php}
// Anpassung der Palette
$GLOBALS['TL_DCA']['tl_member']['palettes']['default'] = str_replace
(
    'company',
    'customer_number,company',
    $GLOBALS['TL_DCA']['tl_member']['palettes']['default']
);

// Hinzufügen der Feld-Konfiguration
$GLOBALS['TL_DCA']['tl_member']['fields']['customer_number'] = array
(
    'label'     => &$GLOBALS['TL_LANG']['tl_member']['customer_number'],
    'exclude'   => true,
    'inputType' => 'text',
    'eval'      => array('mandatory'=>true, 'rgxp'=>'digit', 'maxlength'=>8),
    'sql'       => "varchar(8) NOT NULL default ''"
);
```

Falls Sie den obigen Code nicht verstehen, lesen Sie den Abschnitt über [Data
Container Arrays][1].

Nachdem Sie die Datei abgespeichert haben, müssen Sie die Datenbank 
aktualisieren. Dazu verwenden Sie das [Contao-Installtool][3].


### Eine Übersetzung hinzufügen

Erstellen Sie die Datei `languages/de/tl_member.php` in Ihrem Modulordner und
legen Sie die deutschen Bezeichnungen an:

``` {.php}
$GLOBALS['TL_LANG']['tl_member']['customer_number'] = array
(
    'Kundennummer',
    'Bitte geben Sie die 8-stellige Kundennummer ein.'
);
```

Jetzt können Sie in der Mitgliederverwaltung eine bis zu 8 Ziffern lange
Kundennummer eingeben. Wird das Feld nicht ausgefüllt oder enthält es
nicht-numerische Zeichen, gibt Contao beim Abschicken des Formulars eine
entsprechende Fehlermeldung aus.


## TinyMCE anpassen

Diese Seite erklärt, wie man die Rich Text Editor-Konfiguration anpasst und
updatesicher speichert. Beachten Sie, dass Contao standardmäßig nicht alle
TinyMCE-Plugins enthält und fehlende Ressourcen gegebenenfalls von der
[TinyMCE-Projektwebseite][4] heruntergeladen und in den Ordner
`assets/tinyMCE/plugins` Ihrer Contao-Installation kopiert werden müssen.

![](images/rich-text-editor.jpg?raw=true)

Das obige Bild zeigt die Standardkonfiguration des Editors, die in der Datei
`system/config/tinyMCE.php` hinterlegt ist. Um eine eigene Konfiguration zu
erstellen, duplizieren Sie die Datei, fügen Sie Ihre Änderungen ein und
speichern Sie die neue Datei als `tinyCustom.php`. Passen Sie dann noch die
[DCA-Konfiguration][5] in der Datei `system/config/dcaconfig.php` an, damit
Contao zukünftig die neue Konfigurationsdatei lädt.

``` {.php}
// Die eigene RTE-Konfiguration für Text-Elemente verwenden
$GLOBALS['TL_DCA']['tl_content']['fields']['text']['eval']['rte'] = 'tinyCustom';
```


## Methoden überschreiben

Nehmen wir an, Sie möchten das Navigationsmodul so anpassen, dass es immer
erscheint, selbst wenn keine Unterseiten vorhanden sind und es normalerweise
ausgeblendet würde. In letzterem Fall soll stattdessen ein entsprechender
Hinweis ausgegeben werden. Damit zukünftige Updates ohne Probleme eingespielt
werden können, soll möglichst viel von der Originalklasse erhalten bleiben.
Inhaltselement- und Modulklassen können dynamisch in der Contao-Konfiguration
angegeben und so einfach durch eigene Versionen ersetzt werden.


### Eine eigene Klasse erstellen

Die originale Navigationsklasse verhält sich schon fast so wie gewünscht,
außer dass die Methode `generate()` das Modul ganz ausblendet, wenn keine
Unterseiten vorhanden sind. Da also nur diese eine Methode angepasst werden
muss, empfiehlt es sich, die Originalklasse zu erweitern und einfach zu
überschreiben. Definieren Sie dazu die Klasse `ModuleMyNavigation` in der Datei
`xcustom/ModuleMyNavigation.php`:

``` {.php}
// xcustom/ModuleMyNavigation.php
class ModuleMyNavigation extends ModuleNavigation
{
    public function generate()
    {
        // Die Originalmethode ausführen
        $buffer = parent::generate();

        if (empty($buffer))
        {
            $buffer = 'Keine Unterseiten vorhanden';
        }

        return $buffer;
    }
}
```


### Eine eigene Klasse registrieren

Inhaltselement- und Modulklassen können dynamisch in der Contao-Konfiguration
zugeordnet und so einfach durch eigene Versionen ersetzt werden. Die Namen der
Modulklassen werden im globalen Array `FE_MOD` gespeichert.

``` {.php}
// xcustom/config/config.php
$GLOBALS['FE_MOD']['navigationMenu']['navigation'] = 'ModuleMyNavigation';
```

Dank der dynamischen Konfiguration lädt Contao bei der nächsten Anfrage
automatisch Ihre eigene Klasse und das Navigationsmodul gibt den Hinweis "Keine
Unterseiten vorhanden" aus anstatt gar nicht zu erscheinen. Die Modifikation ist
updatesicher und wartungsfrei.


## Contao-Hooks

Hooks funktionieren ähnlich wie die [Callback-Funktionen][6] des Data Container
Arrays. Sie können eine oder mehrere Funktionen für ein bestimmtes Ereignis
registrieren, die dann bei dessen Eintreten ausgeführt werden. Dadurch lässt
sich der Core um eigene Funktionalität erweitern.


### activateAccount

Der "activateAccount"-Hook wird bei der Aktivierung eines neuen Mitgliederkontos
ausgeführt. Er übergibt das Benutzer-Objekt als Argument und erwartet keinen
Rückgabewert. Hinzugefügt in Version 2.4.3.

``` {.php}
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

``` {.php}
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

``` {.php}
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
und das Widget-Objekt als Argument und erwartet einen boolschen Rückgabewert.
Hinzugefügt in Version 2.6.2.

``` {.php}
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

``` {.php}
// config.php
$GLOBALS['TL_HOOKS']['addLogEntry'][] = array('MyClass', 'myAddLogEntry');

// MyClass.php
public function myAddLogEntry($strText, $strFunction, $strAction)
{
    // Beliebiger Code
}
```


### checkCredentials

Der "checkCredentials"-Hook wird bei der Eingabe eines falschenPassworts bei der
Anmeldung ausgeführt. Er übergibt den Benutzernamenund das Passwort sowie das
Benutzer-Objekt als Argument und erwartet einen boolschenRückgabewert.
Hinzugefügt in Version 2.6.0.

``` {.php}
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

``` {.php}
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


### compileDefinition

Der "compileDefinition"-Hook wird bei der Erstellung einer Formatdefinition in
einem Stylesheet ausgeführt. Er übergibt das Konfigurationsarray als Argument
und erwartet einen String als Rückgabewert. Hinzugefügt in Version 2.9.4.

``` {.php}
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


### createDefinition

Der "createDefinition"-Hook wird beim Import einer Formatdefinition eines
Stylesheets ausgeführt. Er übergibt Schlüssel und Wert, die originale
Formatdefinition sowie das Daten-Array als Argument und erwartet ein Array oder
`false` als Rückgabewert. Hinzugefügt in Version 2.9.4.

``` {.php}
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

``` {.php}
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

``` {.php}
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
eine DCA-Objekt benötigen. Er übergibt den Namen der Aktion und das
DataContainer-Objekt als Argument und erwartet keinen Rückgabewert. Hinzugefügt
in Version 2.6.1.

``` {.php}
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

``` {.php}
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

``` {.php}
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

``` {.php}
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

``` {.php}
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

Der "getContentElement"-Hook wird beim Rendern von Inhaltselementen ausgeführt.
Er übergibt das Datenbankobjekt und den Ausgabe-String als Argument und
erwartet einen Ausgabe-String als Rückgabewert. Hinzugefügt in Version 2.9.0.

``` {.php}
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

``` {.php}
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

``` {.php}
// config.php
$GLOBALS['TL_HOOKS']['getPageIdFromUrl'][] = array('MyClass', 'myGetPageIdFromUrl');

// MyClass.php
public function myGetPageIdFromUrl($arrFragments)
{
    return array_unique($arrFragments);
}
```


### getSearchablePages

Der "getSearchablePages"-Hook wird beim Aufbau des Suchindex ausgeführt. Er
übergibt das URL-Array und die ID der Wurzelseite als Argument und erwartet ein
Array mit absoluten URLs (!) als Rückgabewert. Hinzugefügt in Version 2.2.0.

``` {.php}
// config.php
$GLOBALS['TL_HOOKS']['getSearchablePages'][] = array('MyClass', 'myGetSearchablePages');

// MyClass.php
public function myGetSearchablePages($arrPages, $intRoot)
{
    return array_merge($arrPages, array('Additional pages'));
}
```


### importUser

Der "importUser"-Hook wird beim Antreffen eines unbekannten Benutzernamens
ausgeführt. Er übergibt den Benutzernamen, das Passwort und den Tabellennamen
als Argument und erwartet einen boolschen Rückgabewert. Hinzugefügt in Version
2.7.RC1.

``` {.php}
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


### listComments

Der "listComments"-Hook wird bei der Darstellung von Kommentaren im Backend
ausgeführt. Er übergibt den aktuellen Datensatz als Argument und erwartet
einen String als Rückgabewert. Hinzugefügt in Version 2.8.RC2.

``` {.php}
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

``` {.php}
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

``` {.php}
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

``` {.php}
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

``` {.php}
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

``` {.php}
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

``` {.php}
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

``` {.php}
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


### postDownload

Der "postDownload"-Hook wird nach dem Herunterladen einer Datei mit Hilfe des
Download(s)-Elements ausgeführt. Er übergibt den Dateinamen als Argument und
erwartet keinen Rückgabewert. Hinzugefügt in Version 2.4.6.

``` {.php}
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

``` {.php}
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

``` {.php}
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

``` {.php}
// config.php
$GLOBALS['TL_HOOKS']['postUpload'][] = array('MyClass', 'myPostUpload');

// MyClass.php
public function myPostUpload($arrFiles)
{
    // Beliebiger Code
}
```


### printArticleAsPdf

Der "printArticleAsPdf"-Hook wird beim der Ausgabe eines Artikels im PDF-Format
ausgeführt. Er übergibt den Artikeltext und das Artikelobjekt  als Argument
und erwartet keinen Rückgabewert. Hinzugefügt in Version 2.8.RC1.

``` {.php}
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
Er übergibt das Datenarray, das [Data Container Array][1] und das Dateiarray
als Argument und erwartet keinen Rückgabewert. Hinzugefügt in Version 2.4.4.

``` {.php}
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

``` {.php}
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

``` {.php}
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

``` {.php}
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
Argument und erwartet einen boolschen Rückgabewert. Geben Sie `true` zurück,
um die Seite neu zu laden. Hinzugefügt in Version 2.6.4.

``` {.php}
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

``` {.php}
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

``` {.php}
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


[1]: 06-Data-Container-Arrays.md
[2]: http://en.wikipedia.org/wiki/List_of_ISO_639-1_codes
[3]: 01-Installation.md#das-contao-installtool
[4]: http://tinymce.moxiecode.com
[5]: 07-Customizing-Contao.md#die-dca-konfiguration-anpassen
[6]: 06-Data-Container-Arrays.md#callbacks
