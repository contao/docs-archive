# Eigene Inserttags entwickeln

Nachfolgend wird beschrieben, wie man eigene Inserttags programmiert und
welche Dinge dabei zu beachten sind.


## Kurze Einführung 

Contao bietet die Möglichkeit, mittels so genannter Inserttags (Platzhalter)
beim Laden der Webseite bestimmte Inhalte zu ersetzen. Ist der Seiten Cache
eingeschaltet, werden eigene Inserttags ersetzt vor der Abspeicherung der
Seite im Cache.  Es ist jedoch möglich, daß der Inserttag Platzhalter selbst
im Cache  gespeichert wird und dieser dann erst direkt vor Auslieferung an den
Browser ersetzt wird mittels einem Präfix "cache_".   
Beides wird im Code-Beispiel erläutert.


## Eigene Inserttags erstellen  

Um Inserttags nutzen zu können und demzufolge auch eigene Inserttags
anzubieten, gibt es in Contao einen Hook "replaceInsertTags ". Um eine eigenen
Inserttag zu erstellen muss man den Ablauf kennen:

1. Contao parst den Seiteninhalt und stößt dabei auf einen Inserttag
2. Contao versucht diesen Inserttag mit den Core-Möglichkeiten zu ersetzen 
3. Wenn Contao den Inserttag nicht kennt, wird es an den Hook 
    "replaceInsertTags" weitergereicht.

Dieser Hook erhält das unbekannte Inserttag als Parameter. Der Entwickler
muss nun prüfen ob er das unbekannte Inserttag ersetzen möchte. Wenn ja, gibt
er einen beliebigen Content zurück. Wenn der Entwickler nichts mit dem
unbekannten Inserttag anfangen kann, so muss `false` zurück gegeben werden.
Wird das nicht getan, ist die gesamte Hook Kette unterbrochen, nachfolgende
Erweiterungen die ebenfalls Inserttags anbieten werden dann nicht mehr
aufgerufen!


## Code-Beispiel

In diesem Code-Beispiel soll der Inserttag {{foo::bar}} ersetzt werden durch
das Modul "myinserttag". Als erstes muss der Hook registriert werden.

``` {.php}
// Datei /system/modules/myinserttag/config/config.php
 
 // Registrieren im Hooks replaceInsertTags
$GLOBALS['TL_HOOKS']['replaceInsertTags'][] = array('MyClass', 'myReplaceInsertTags');
```

Nach der Registrierung im Hook, muss eine Klasse erstellt werden, welche eine
Methode zur Ersetzung beinhaltet. Dabei muss der Name der Klasse und der
Methode identisch sein wie bei der Hook Registration. Außerdem muss der Name
der Datei (ohne Endung) identisch sein wie der Name der Klasse.

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
        } else {
            return 'Fehler! foo ohne Parameter!';
        }
    }
 }
 ```

Wenn man einen zweigeteilten Inserttag verwendet, splittet man den Tag mittels
`explode` anhand des Gültigkeitsbereichsoperator  `::`.  Die geschweiften
Klammern werden bereits von Contao entfernt und müssen daher nicht mehr
entfernt werden. Im Code-Beispiel wurde zusätzlich noch eine Ausgabe
ermöglicht, wenn der Parameter "bar" nicht angegeben wurde.
