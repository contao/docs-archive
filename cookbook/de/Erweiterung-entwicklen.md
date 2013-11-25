Erweiterung entwicklen
======================

Für das Testen der Erweiterung auf einer lokalen Contao-Installation in den Einstellungen (Backend:
_System_ -> _Einstellungen_) die beiden folgenden Optionen aktivieren:

- _Globale Einstellungen_ -> _Internen Cache umgehen_
- _Sicherheitseinstellungen_ -> _Fehlermeldungen anzeigen_

Den Button _Speichern_ bzw. _Speichern und schließen_ nicht vergessen.

Zur Sicherheit im Anschluss den internen Cache noch mal leeren. Das geht im Backend im Punkt
_System_ -> _Systemwartung_. Auf dieser Seite _Daten bereinigen_ -> _Internen Cache leeren_
auswählen und den den Button _Daten bereinigen_ nicht vergessen.


Best Practices
==============


Verwenden der Entwickler-Tools
------------------------------

Mit dem _Extension-Creator_ im Backend kann ein Grundgerüst für eigene Contao-Erweiterungen angelegt
werden.

__Achtung:__ Nach dem Anlegen dieses Grundgerüsts und auch nach dem Hinzufügen neuer Klassen, immer
im Backend mit dem _Autoload-Creator_ die Datei `autoload.php` aktualisieren, damit alle Klassen der
Erweiterung gefunden werden können.


Lernen durch Kopieren
---------------------

Wenn man eine ähnliche Funktion implementieren möchte, wie sie in Contao oder einer anderen
Erweiterung bereits besteht, dort im Quelltext nachsehen, wie sie implementiert ist. Versuchen das
Muster zu verstehen und dann das Muster kopieren und für den eigenen Zweck anpassen.


Namespaces
----------

[Auf Empfehlung vom Contao Team](https://community.contao.org/de/showthread.php?30961-Contao-3-und-Namespace&p=203762&viewfull=1#post203762)
sollten Namespace in Erweiterungen für Contao nicht verwendet werden.

Der Grund dafür ist dass Namespaces in Contao, nicht wie von Programmiersprachen vorgesehen, zur
Unterteilung des globalen Namespaces und zur Paketierung von Softwaremodulen verwendet werden. In
Contao wurden Namespaces nur eingeführt, um die Klassen des Cores ersetzen zu können.

Durch den Verzicht auf Namespaces erspart man sich den Ärger, dass Klassen womöglich nicht korrekt
oder gar nicht geladen werden können.


Model
-----

Das mit Contao 3 eingeführte Model ist die erste Implementierung eines OR-Mapper (
[object-relational mapping](http://de.wikipedia.org/wiki/Objektrelationale_Abbildung)) in Contao.

Das Contao Model reicht nicht an bestehenden OR-Mapper wie _JPA_ (Java Persistence API) für Java
oder _Core Data_ für Cocoa unter iOS und Mac OS X heran. Man muss aber dazusagen das die JPA und
Core Data seit Jahren mit für Contao unmöglicher Man Power beständig weiterentwickelt wird. Mit der
Zeit und Unterstützung der Community wird Contao diesen Vorsprung sicher in der Zukunft verkürzen
können ;-)

Der Extension-Creator erzeugt für Frontend-Tabellen eine dazugehörige Model-Klasse im Verzeichnis
`models` der Erweiterung. Diese Klasse kann ohne weitere Anpassung über die folgenden statischen
Methoden genutzt werden:

- `findByPk` - Gibt ein Objekt zu einem Schlüsselwert zurück, es wird dabei der Primary Key der
  Tabelle verwendet.
- `findByIdOrAlias`- Gibt ein Objekt anhand seiner ID oder seines Aliases zurück; als Alternative zu
  `findByPk` verwendet diese Methode die Spalten `id` und `alias`; nützlich für alle Objekte die
  über eine URL erreichbar sind.
- `findByPk` - Gibt alle Objekte dieses Typs zurück.

Methoden die nur ein Objekt zurück geben, geben dies direkt zurück. Methoden die mehrere Objekte
zurückgeben, geben diese als `Contao\Model\Collection` verpackt zurück.

Es gibt noch weitere Methoden die die Suche nach Objekten über Suchkriterien einschränken. Diese
Methoden schaut man sich am besten in der Klasse `Contao\Model` an.

Um effektiver mit dem Model zu arbeiten, sollte man sich in der eigenen Model-Klasse weitere
statische Methoden definieren. Diese folgen dem Muster:

- `findPublishedByFoo` - Zur Suche nach Objekte, die für die Property (=Tabellenspalte) _Foo_ einen
  bestimmten Wert haben.
- `coundPublishedByFoo` - Zum Zählen der Objekte, die für die Property (=Tabellenspalte) _Foo_ einen
  bestimmten Wert haben.

__Achtung:__ Die _find_-Methoden geben `null` zurück, wenn es keine Objekte gibt, die dem
angegebenen Kriterien entsprechen. In Contao 4 soll das geändert werden, so das statt `null` eine
leere Collection zurückgegeben wird
([GutHub Issue #6147](https://github.com/contao/core/issues/6147)).
