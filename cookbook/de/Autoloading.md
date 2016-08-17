# Autoloading in Contao 3

> #### warning:: Vorsicht
> Diese Informationen beziehen sich auf Contao 3.  
> Contao 4 verwendet den Composer Class Loader nach [PSR-0][1] 
> bzw. [PSR-4][2] Standard.

## Einführung

Der Contao ClassLoader bietet die Möglichkeit, beliebige Klassen in der
lokalen Umgebung durch eigene Versionen zu überschreiben, wobei Methoden
der Ursprungsklasse geerbt werden können.

Contao verwendet dazu die PHP-Funktion `class_alias`, mit welcher
eine Klasse unter einem zusätzlichen Namen registriert werden kann.

Aus den genannten Umständen unterstützt der ClassLoader kein Autoloading
nach PSR-0.

> #### danger:: Achtung 
> Die Überschreibung von Core-Klassen ist nur für lokale Anpassungen
> vorgesehen! Keinesfalls sollten entsprechende Erweiterungen im Extension
> Repository veröffentlicht werden, da dabei sehr schnell Konflikte entstehen.


### Beispiel

Contao liefert die Klasse `Controller` im Namespace `Contao`.
Der eindeutige Name der Klasse ist also `\Contao\Controller`. Mittels
`class_alias` wird der Vendor-Präfix (hier `Contao`) abgeschnitten und die
Klasse nur noch als `\Controller` verwendet.

In einer eigenen Erweiterung kann nun die Klasse
`class VendorExample\Controller extends \Contao\Controller` erstellt werden.
Die Beispielklasse erbt alle Methoden von `\Contao\Controller`, lediglich
die Methode `loadDataContainer` wird mit einer eigenen Version ersetzt.
Da die Klasse nach Anwendung von `class_alias` auch den Namen `\Controller`
erhält, wird sie anstelle der Core-Klasse vom System verwendet.


### Wo befinden sich die Definitionen?

Die Definitionen zum Autoloader befinden sich innerhalb jeder Erweiterung
im Verzeichnis `config`.


## autoload.ini

### Abhängigkeiten definieren

Der Schlüssel `requires` bestimmt, von welchen anderen Erweiterungen
die Erweiterung abhängig ist. Die Erweiterungen werden dann in der
entsprechenden Reihenfolge geladen. Es können beliebig viele 
`requires` angegeben werden.
 
```ini
requires[] = "core"
```

### Konfiguration

Die Schlüssel `register_namespaces`, `register_classes` und 
`register_templates` bestimmen, ob der Autoload Generator diese Bereiche
beim Generieren der `autoload.php` berücksichtigen soll.

```ini
register_namespaces = true
register_classes    = true
register_templates  = true
```

### Ausnahmen

Die Schlüssel `register_namespaces`, `register_classes` und 
`register_templates` im Zusammenhang mit einzelnen Unterordnern
bestimmen, ob der Autoload Generator diese Bereiche
beim Generieren der `autoload.php` berücksichtigen soll.

```ini
[vendor/*]
register_namespaces = false
register_classes    = false
register_templates  = false
```


## autoload.php

Die `autoload.php` kann, sofern erwünscht, vom Autoloader basierend
auf der `autoload.ini` generiert werden. Natürlich kann man diese
aber genauso von Hand schreiben.

### Namespaces registrieren

Mit der statischen Methode `addNamespaces` werden zusätzliche Namespaces
registriert. Nutzt man z.B. eine Klasse `VendorExample\ClassXY.php`
im Projekt, registriert man hier den Namespace `VendorExample`.

```php
ClassLoader::addNamespaces(array
(
    'VendorExample'
));
```

### Klassen registrieren

Um die Klasse `VendorExample\ClassXY.php` aus dem Verzeichnis
`system/modules/vendor_example/modules` zu nutzen, muss diese mittels
der statischen Methode `addClasses` registriert werden.

```php
ClassLoader::addClasses(array
(
   'VendorExample\ClassXY' => 'system/modules/vendor_example/modules/ClassXY.php' 
));
```

### Templates registrieren

Um ein Template `template.html5` bzw. `template.xhtml` aus dem Verzeichnis
`system/modules/vendor_example/templates/modules` zu nutzen, muss dieses
mittels der statischen Methode `addFiles` registriert werden.

```php
TemplateLoader::addFiles(array
(
    'mod_example' => 'system/modules/vendor_example/templates/modules'
));
```


[1]: http://www.php-fig.org/psr/psr-0/
[2]: http://www.php-fig.org/psr/psr-4/
