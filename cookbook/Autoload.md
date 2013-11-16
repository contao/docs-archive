# Autoloading

Die Definitionen zum Autloader befinden sich innerhalb jeder Erweiterung im Verzeichnis `config`

## autoload.ini

### Abhängigkeiten definieren

Der Schlüssel `requires` bestimmt, von welchen anderen Erweiterungen meine Erweiterung abhängig ist
 
``` {.ini}
requires[] = "core"
```

### Konfiguration

Die Schlüssel `register_namespaces`, `register_classes` und 
`register_templates` bestimmen, ob der Autoload Generator diese Bereiche beim `autoload.php` generieren berücksichtigen soll.

``` {.ini}
register_namespaces = true
register_classes    = true
register_templates  = true
```

### Ausnahmen

Die Schlüssel `register_namespaces`, `register_classes` und 
`register_templates` im Zusammenhang mit einzelnen `vendors` bestimmen, ob der Autoload Generator diese Bereiche beim `autoload.php` generieren berücksichtigen soll.

``` {.ini}
[vendor/*]
register_namespaces = false
register_classes    = false
register_templates  = false
```

## autoload.php

Die `autoload.php` kann, sofern erwünscht vom Autoloader basieren auf der `autoload.ini` generiert werden. Es ist, aber auch möglich diese von Hand zu schreiben.

### Namespaces registrieren

Mit der statischen Methode `addNamespaces` kann man sich zusätzliche Namespaces registrieren. Wenn man jetzt z.B. eine Klasse `Vendor\Project\ClassXY.php` im Projekt nutzen will, registiert man hier den Namespace `Vendor\Project`

``` {.php}
ClassLoader::addNamespaces(array
(
    'Vendor\Project'
));
```

### Klassen registrieren

Um z.B. die Klasse `Vendor\Project\ClassXY.php` aus dem Verzeichnis `system/modules/vendor_project/modules` zu nutzen, nutzt man folgende statische Methode: `addClasses`

``` {.php}
ClassLoader::addClasses(array
(
   'Vendor\Project\ClassXY' => 'system/modules/vendor_project/modules/ClassXY' 
));
```

### Templates registrieren

Um z.B. ein Template `template.html5` bzw. `template.xhtml` aus dem Verzeichnis `system/modules/vendor_project/templates/modules` zu nutzen, nutzt man folgende statische Methode: `addFiles`

``` {.php}
TemplateLoader::addFiles(array
(
    'template' => 'system/modules/vendor_project/templates/modules'
));
```
