# Eigene Inserttags entwickeln

Nachfolgend wird beschrieben, wie man eigene Inserttags programmiert und
welche Dinge dabei zu beachten sind.


## Kurze Einführung 

Contao bietet die Möglichkeit, mittels so genannter Inserttags (Platzhalter)
beim Laden der Webseite bestimmte Inhalte zu ersetzen. Ist der Seiten Cache
eingeschaltet, werden eigene Inserttags ersetzt vor der Abspeicherung der
Seite im Cache.  Es ist jedoch möglich, dass der Inserttag Platzhalter selbst
im Cache  gespeichert wird und dieser dann erst direkt vor Auslieferung an den
Browser ersetzt wird mittels einem Präfix "cache_".   
Beides wird im Code-Beispiel erläutert.


## Eigene Inserttags erstellen  

Um Inserttags nutzen zu können und demzufolge auch eigene anzubieten, gibt es
in Contao einen Hook "replaceInsertTags ". Um ein eigenes Inserttag zu
erstellen, muss man den Ablauf kennen:

1. Contao parst den Seiteninhalt und stößt dabei auf ein Inserttag
2. Contao versucht dieses Inserttag mit den Core-Möglichkeiten zu ersetzen
3. Wenn Contao das Inserttag nicht kennt, wird es an den Hook
    "replaceInsertTags" weitergereicht.

Dieser Hook erhält das unbekannte Inserttag als Parameter. Der Entwickler
muss nun prüfen, ob er das unbekannte Inserttag ersetzen möchte. Wenn ja, gibt
er einen beliebigen Content zurück. Wenn der Entwickler nichts mit dem
unbekannten Inserttag anfangen kann, so muss `false` zurück gegeben werden.
Wird das nicht getan, ist die gesamte Hook Kette unterbrochen, nachfolgende
Erweiterungen die ebenfalls Inserttags anbieten werden dann nicht mehr
aufgerufen!


## Code-Beispiel

In diesem Code-Beispiel soll das Inserttag {{foo::bar}} ersetzt werden durch
das Modul "myinserttag". Als erstes muss der Hook registriert werden.

``` {.php}
// Datei /system/modules/myinserttag/config/config.php
 
// Registrieren im Hooks replaceInsertTags
$GLOBALS['TL_HOOKS']['replaceInsertTags'][] = array('MyClass', 'myReplaceInsertTags');
```

Nach der Registrierung im Hook muss eine Klasse erstellt werden, welche die
Methode zur Ersetzung beinhaltet. Dabei muss der Name der Klasse und der
Methode identisch sein wie bei der Hook Registration. Außerdem muss der Name
der Datei (ohne Endung) identisch sein mit dem Name der Klasse.

``` {.php}
// Datei /system/modules/myinserttag/MyClass.php
 
class MyClass extends Frontend
{
    public function myReplaceInsertTags($strTag)
    {
        // Parameter abtrennen
        $arrSplit = explode('::', $strTag);
 
        if ($arrSplit[0] != 'foo' && $arrSplit[0] != 'cache_foo')
        {
            //nicht unser Inserttag
            return false;
        }
        
        // Parameter angegeben?
        if (isset($arrSplit[1]) && $arrSplit[1] == 'bar')
        {
            return 'Parameter bar';
        }
        else
        {
            return 'Fehler! foo ohne Parameter!';
        }
    }
}
```

Wenn man ein zweigeteiltes Inserttag verwendet, splittet man das Tag mittels
`explode` anhand des Gültigkeitsbereichsoperators  `::`. Die geschweiften
Klammern werden bereits von Contao entfernt und müssen daher nicht mehr
entfernt werden. Im Code-Beispiel wurde zusätzlich noch eine Ausgabe
erzeugt, wenn der Parameter "bar" nicht angegeben wurde.

Damit Contao 3 die Klasse findet, muss nun im Backend der Autoload
Generator für dieses Modul aufgerufen werden, um die autoload.php im config
Verzeichnis zu generieren.


## Code-Beispiel mit Namespace

Ist die Klasse innerhalb eines Namespaces, ändert sich die Syntax ein wenig.
Ansonsten gelten die selben, bereits genannten Hinweise.

``` {.php}
 // Datei /system/modules/myinserttag/config/config.php
 
 // Registrieren im Hooks replaceInsertTags
 $GLOBALS['TL_HOOKS']['replaceInsertTags'][] = array('MyModule\MyClass', 'myReplaceInsertTags');
```

``` {.php}
// Datei /system/modules/myinserttag/MyClass.php
 
/**
* Run in a custom namespace, so the class can be replaced
*/
namespace Vendor\MyModule;

class MyClass extends \Frontend
{
    public function myReplaceInsertTags($strTag)
    {
        // Parameter abtrennen
        $arrSplit = explode('::', $strTag);
 
        if ($arrSplit[0] != 'foo' && $arrSplit[0] != 'cache_foo')
        {
            //nicht unser Inserttag
            return false;
        }
        // Parameter angegeben?
        if (isset($arrSplit[1]) && $arrSplit[1] == 'bar')
        {
            return 'Parameter bar';
        } else {
            return 'Fehler! foo ohne Parameter!';
        }
    }
}
```
