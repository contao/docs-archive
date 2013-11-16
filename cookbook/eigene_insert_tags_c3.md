# Eigene Insert-Tags entwickeln
Nachfolgend wird beschrieben, wie man eigene Insert-Tags programmiert und welche Dinge dabei zu beachten sind.


# Kurze Einführung
Contao bietet die Möglichkeit, mittels so genannter Insert-Tags (Platzhalter) beim Laden der Webseite bestimmte Inhalte zu ersetzen. Ist der Seiten Cache eingeschaltet, werden eigene Insert-Tags ersetzt vor der Abspeicherung der Seite im Cache. Es ist jedoch möglich, daß der Insert-Tag Platzhalter selbst im Cache gespeichert wird und dieser dann erst direkt vor Auslieferung an den Browser ersetzt wird mittels einem Präfix "cache_". Beides wird im Code Beispiel erläutert.


# Eigene Insert-Tags erstellen 
Um Insert-Tags nutzen zu können und demzufolge auch eigene anzubieten, gibt es in Contao einen Hook "replaceInsertTags ".
Um eine eigenen Insert-Tag zu erstellen muss man den Ablauf kennen:
1. Contao parsed einen Seitenaufruf und stößt dabei auf ein Insert-Tag
2. Contao probiert dieses Insert-Tag mit den Core-Möglichkeiten zu ersetzen
3. Wenn Contao den Insert-Tag nicht kennt, wird es an den Hook "replaceInsertTags" weitergereicht. 

Dieser Hook erhält das unbekannte Insert-Tag als Parameter. Der Entwickler muss nun prüfen ob er das unbekannte Insert-Tag ersetzen möchte. Wenn ja, gibt er einen beliebigen Content zurück.
Wenn der Entwickler nichts mit dem unbekannten Insert-Tag anfangen kann, so muss `false` zurück gegeben werden. Wird das nicht getan, ist die gesamte Hook Kette unterbrochen, nachfolgende Erweiterungen die ebenfalls Insert-Tag anbieten werden dann nicht mehr aufgerufen!


# Code-Beispiel
In diesem Code-Beispiel soll der Insert-Tag {{foo::bar}} ersetzt werden durch das Modul "myinserttag". Als erstes muss der Hook registriert werden. 

``` {.php}
<?php 
 // Datei /system/modules/myinserttag/config/config.php
 
 // Registrieren im Hooks replaceInsertTags
 $GLOBALS['TL_HOOKS']['replaceInsertTags'][] = array('MyClass', 'myReplaceInsertTags');
?>
```

Nach der Registrierung im Hooks muss eine Klasse erstellt werden, welche eine Methode zur Ersetzung beinhaltet.
Dabei muss der Name der Klasse und der Methode identisch sein wie bei der Hook Registration.
Außerdem muss der Name der Datei (ohne Endung) identisch sein wie der Name der Klasse. 

``` {.php}
<?php 
 // Datei /system/modules/myinserttag/MyClass.php
 
 class MyClass extends Frontend
 {
    public function myReplaceInsertTags($strTag)
    {
        // Parameter abtrennen
        $arrSplit = explode('::', $strTag);
 
        if ($arrSplit[0] != 'foo' || $arrSplit[0] == 'cache_foo')
        {
            //nicht unser Insert-Tag
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
?>
```

Wenn man einen zweigeteilten Insert-Tag verwendet, splittet man den Tag mittels `explode` anhand des Gültigkeitsbereichsoperator  `::`. Die geschweiften Klammern werden bereits von Contao entfernt und müssen daher nicht mehr entfernt werden.
Im Code-Beispiel wurde zusätzlich noch eine Ausgabe ermöglicht, wenn der Parameter "bar" nicht angegeben wurde.

Damit Contao 3 nun die Klasse findet, muss nun im Backend der Autoload Generator für dieses Modul aufgerufen werde um die autoload.php zu generieren im config Verzeichnis. 
