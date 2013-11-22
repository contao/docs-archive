# Autoloading

## Hinweis
Der Contao Autoloader unterstützt Namespaces nach dem Schema
`VendorExample\ClassXY`, dh. einen Vendorprefix und den Klassennamen,
längere Namespaces werden nicht unterstützt. Die Klassen werden
im Rootnamespace registriert, so dass sie per`\ClassXY`verfügbar ist, damit ist
es möglich sämtliche Core Klassen, oder auch jene von anderen Erweiterungen zu
überschreiben. Es ist kein Autoloading nach PSR-0 möglich.

## Wo befinden sich die Definitionen?
Die Definitionen zum Autoloader befinden sich innerhalb jeder Erweiterung
im Verzeichnis `config`

## autoload.ini

### Abhängigkeiten definieren

Der Schlüssel `requires` bestimmt, von welchen anderen Erweiterungen
die Erweiterung abhängig ist
 
``` {.ini}
requires[] = "core"
```

### Konfiguration

Die Schlüssel `register_namespaces`, `register_classes` und 
`register_templates` bestimmen, ob der Autoload Generator diese Bereiche
beim generieren der `autoload.php` berücksichtigen soll.

``` {.ini}
register_namespaces = true
register_classes    = true
register_templates  = true
```

### Ausnahmen

Die Schlüssel `register_namespaces`, `register_classes` und 
`register_templates` im Zusammenhang mit einzelnen `vendors` bestimmen,
ob der Autoload Generator diese Bereiche
beim generieren der `autoload.php` berücksichtigen soll.

``` {.ini}
[vendor/*]
register_namespaces = false
register_classes    = false
register_templates  = false
```

## autoload.php

Die `autoload.php` kann, sofern erwünscht vom Autoloader basieren
auf der `autoload.ini` generiert werden. Es ist aber auch möglich diese
von Hand zu schreiben.

### Namespaces registrieren

Mit der statischen Methode `addNamespaces` kann man sich zusätzliche
Namespaces registrieren. Wenn man jetzt z.B. eine Klasse `VendorExample\ClassXY.php`
im Projekt nutzen will, registiert man hier den Namespace `VendorExample`

``` {.php}
ClassLoader::addNamespaces(array
(
    'VendorExample'
));
```

### Klassen registrieren

Um z.B. die Klasse `VendorExample\ClassXY.php` aus dem Verzeichnis
`system/modules/vendor_example/modules` zu nutzen, nutzt man folgende
statische Methode: `addClasses`

``` {.php}
ClassLoader::addClasses(array
(
   'VendorExample\ClassXY' => 'system/modules/vendor_example/modules/ClassXY.php' 
));
```

### Templates registrieren

Um z.B. ein Template `template.html5` bzw. `template.xhtml` aus dem Verzeichnis
`system/modules/vendor_example/templates/modules` zu nutzen, nutzt man folgende
statische Methode: `addFiles`

``` {.php}
TemplateLoader::addFiles(array
(
    'mod_example' => 'system/modules/vendor_example/templates/modules'
));
```