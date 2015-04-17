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

```php
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

```php
// xcustom/config/config.php
$GLOBALS['FE_MOD']['navigationMenu']['navigation'] = 'ModuleMyNavigation';
```

Dank der dynamischen Konfiguration lädt Contao bei der nächsten Anfrage
automatisch Ihre eigene Klasse und das Navigationsmodul gibt den Hinweis "Keine
Unterseiten vorhanden" aus anstatt gar nicht zu erscheinen. Die Modifikation ist
updatesicher und wartungsfrei.
