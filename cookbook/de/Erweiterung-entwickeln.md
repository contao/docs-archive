# Erweiterung entwicklen

> #### warning:: Vorsicht 
> Diese Anleitung bezieht sich auf die Entwicklung von Erweiterungen
> für Contao 3. Contao 4 verwendet Symfony Bundles, eine Einführung zu Bundles
> ist im [Symfony Handbuch][1] zu finden.

Für das Testen der Erweiterung auf einer lokalen Contao-Installation in den
Einstellungen (Backend: _System_ -> _Einstellungen_) die beiden folgenden
Optionen aktivieren:

- _Globale Einstellungen_ -> _Internen Cache umgehen_
- _Sicherheitseinstellungen_ -> _Fehlermeldungen anzeigen_

Den Button _Speichern_ bzw. _Speichern und schließen_ nicht vergessen.

Zur Sicherheit im Anschluss den internen Cache noch mal leeren. Das geht im
Backend im Punkt _System_ -> _Systemwartung_. Auf dieser Seite _Daten
bereinigen_ -> _Internen Cache leeren_ auswählen und den den Button _Daten
bereinigen_ nicht vergessen.


# Best Practices


## Verwenden der Entwickler-Tools

Mit dem _Extension-Creator_ im Backend kann ein Grundgerüst für eigene
Contao-Erweiterungen angelegt werden.

Die Datei `autoload.php` konfiguriert das Finden und Laden der Klassen innerhalb
von Contao. In [Autoloading](Autoloading.md) ist die Konfiguration näher
beschrieben.

> #### hint:: Anmerkung 
> Nach dem Anlegen dieses Grundgerüsts und auch nach dem Hinzufügen neuer 
> Klassen, immer im Backend mit dem _Autoload-Creator_ die Datei `autoload.php` 
> aktualisieren, damit alle Klassen der Erweiterung gefunden werden können.


## Lernen durch Kopieren

Wenn man eine ähnliche Funktion implementieren möchte, wie sie in Contao oder
einer anderen Erweiterung bereits besteht, sieht man am besten dort im Quelltext
nach, wie sie implementiert ist. Dabei sollte man den Quelltext nicht einfach
kopieren, sondern versuchen das Muster zu verstehen und so das Muster für den
eigenen Zweck leichter anpassen zu können.


## Namespaces

[Auf Empfehlung vom Contao Team](https://community.contao.org/de/showthread.php?30961-Contao-3-und-Namespace&p=203762&viewfull=1#post203762)
sollten Namespace in Erweiterungen für Contao nicht verwendet werden.

Der Grund dafür ist dass Namespaces in Contao, nicht wie von Programmiersprachen
vorgesehen, zur Unterteilung des globalen Namespaces und zur Paketierung von
Softwaremodulen verwendet werden. In Contao wurden Namespaces nur eingeführt, um
die Klassen des Cores ersetzen zu können.

Durch den Verzicht auf Namespaces erspart man sich den Ärger, dass Klassen
womöglich nicht korrekt oder gar nicht geladen werden können.

> #### danger:: Achtung! 
> Contao 4 verwendet echte Namespaces nach PSR-0/PSR-4.


## Model

Das mit Contao 3 eingeführte Model ist die erste Implementierung eines OR-Mapper
([object-relational mapping](http://de.wikipedia.org/wiki/Objektrelationale_Abbildung))
in Contao.

__Anmerkung:__ Das Contao Model reicht nicht an bestehenden OR-Mapper wie _JPA_
(Java Persistence API) für Java oder _Core Data_ für Cocoa unter iOS und
Mac OS X heran. Man muss aber dazusagen das die JPA und Core Data seit Jahren
mit für Contao unmöglicher Man Power beständig weiterentwickelt wird. Mit der
Zeit und Unterstützung der Community wird Contao diesen Vorsprung sicher in der
Zukunft verkürzen können ;-)

Der Extension-Creator erzeugt für Frontend-Tabellen eine dazugehörige
Model-Klasse im Verzeichnis `models` der Erweiterung. Diese Klasse kann ohne
weitere Anpassung über die folgenden statischen Methoden genutzt werden:

- `findByPk` - Gibt ein Objekt zu einem Schlüsselwert zurück, es wird dabei der
  Primary Key der Tabelle verwendet.
- `findByIdOrAlias` - Gibt ein Objekt anhand seiner ID oder seines Aliases
  zurück; als Alternative zu `findByPk` verwendet diese Methode die Spalten `id`
  und `alias`; nützlich für alle Objekte die   über eine URL erreichbar sind.
- `findByAll` - Gibt alle Objekte dieses Typs zurück.

Methoden die nur ein Objekt zurück geben, geben dies direkt zurück. Methoden die
mehrere Objekte zurückgeben, geben diese als `Contao\Model\Collection` verpackt
zurück.

Mehr Informationen zur Erstellung und Nutzung von Modellklassen finden sich im
[Models-Tutorial](Models.md)

> #### hint:: Anmerkung 
> In der Klassendokumentation der Modellklasse können mit `@property` die
> Eigenschaften (=Spalten) des Modells dokumentiert werden. Moderne IDEs bieten
> dann bei der Codevervollständigung diese Felder mit an.

Um effektiver mit dem Model zu arbeiten, sollte man sich in der eigenen
Model-Klasse weitere statische Methoden definieren. Diese folgen dem Muster:

- `findByFoo` - Zur Suche nach Objekte, die für die Property (=Tabellenspalte)
  _Foo_ einen bestimmten Wert haben.
- `findPublishedByFoo` - Zur Suche nach allen veröffentlichten Objekte, die für
  die Property (=Tabellenspalte) _Foo_ einen bestimmten Wert haben.
- `countByFoo` - Zum Zählen der Objekte, die für die Property (=Tabellenspalte)
  _Foo_ einen bestimmten Wert haben.

> #### warning:: Vorsicht 
> Die _find_-Methoden geben `null` zurück, wenn es keine Objekte
> gibt, die dem angegebenen Kriterien entsprechen. In Contao 4 soll das geändert
> werden, so das statt `null` eine leere Collection zurückgegeben wird
> ([GitHub Issue #6147](https://github.com/contao/core/issues/6147)).

  -
> #### info:: Info 
> Wie man die Toggle-Funktion für die Veröffentlichung von Inhalten im
> Backend implementiert, wird in
> [Toggle Funktion in eigenen Erweiterungen](Toggle-Funktion-in-eigenen-Erweiterungen.md)
> beschrieben.


## Frontend-Module

Das Model liefert entweder eine `Model`-Instanz oder eine `Collection`-Instanz
die man direkt im Frontend-Template verwenden kann. Besser ist es jedoch die
Logik zum Lesen aus dem Model soweit wie möglich in der Frontend-Klasse zu
lassen und im Template nur Strings zu verwenden.

Um eine Liste von Objekten vom Typ _Foo_ im Frontend darzustellen, sind drei
Methoden in der Frontend-Klasse notwendig:

- `compile` - Verwendet die _findBy_-Methoden des Models zum Bestimmen der
  anzuzeigenden Objekte und delegiert dann `parseFoos`.
- `parseFoos` - Iteriert über alle gefunden Objekte und delegiert an `parseFoo`
  um für jedes Objekt einen String zu bestimmen. Die Methode gint ein Array von
  Strings zurück, ein String pro Objekt der Collection. Gibt es keine Objekte,
  gibt die Methode ein leeres Array zurück.
- `parseFoo` - Erzeugt zu einem Objekt seine Repräsentation als String.

Bei diesem Muster sind zwei Templates beteiligt. Eines für das Frontend-Modul
`mod_foo`, welches in der Variablen `$strTemplate` der Frontend-Klasse
deklariert ist. Ein zweites Template wird in der Methode `parseFoo` geladen,
nennen wir es `foo`.

Im Template `mod_foo` werden mit einer Schleife die Objekte angezeigt:

```php
<?php foreach ($this->foos as $foo) echo $foo; ?>
```

Im Template `foo` ist nur das für ein einzelnes Objekt notwendige HTML
enthalten:

```php
<h2><?php echo $this->title; ?></h2>
<p><?php echo $this->description; ?></p>
```

Somit hat man nicht nur eine elegante Überführung des Models auf Strings für das
Template, sondern das Template wird dabei noch in handliche Bausteine zerlegt.

So lässt z.B. sich der Template-Baustein für ein Objekt, abhängig von seine Typ
in der `parseFoos` variieren. Auch das Überscheiben von Templates durch Designer
wird einfacher, weil im Template weniger Logik enthalten ist und nur mit
Platzhaltern gearbeitet werden kann.



[1]: http://symfony.com/doc/current/cookbook/bundles/index.html
