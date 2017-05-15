# Pakete / Erweiterungen mit dem Contao Manager verwalten

## Pakete aktualisieren
Mit einem Klick auf den die Schaltfläche *Update Packages* werden alle installieren Pakete auf den aktuellen Stand gebracht.
D.h. dabei wird auch Contao 4 auf die aktuellste Version aktualisiert.

##  Pakete suchen
Klicken Sie dazu auf *Search packages* und tippen anschließend Ihren gewünschten Suchbegriff in das Suchfeld.
Mit den Optionen *Contao 4 bundels* und *Contao 3 extensions* kann festgelegt werden, nach welchen Paketen gesucht wird.

Je nachdem, ob der Entwickler seine Erweiterung schon als natives *Contao 4 bundle* erstellt hat, müssen Sie ggf. auf *Contao 3 extensions* umschalten.
Der Contao Manager kann nur Pakete finden, die über packagist.org gelistet sind.

## Pakete installieren
Sie sollten nun eine Liste an Erweiteurngen angezeigt bekommen. Wählen Sie das gewünschte Paket aus und klicken auf *Check & Install*.

Es erscheint nun die Möglichkeit eine bestimmte Version festzulegen. Klicken SIe dazu auf das Zahnradsymbol und tippen die gewünschte Version ein.
In Normalfall ist dies allerdings nicht nötig und Sie klicken auf *Apply changes*.

Nun startet der Contao Manager einen Task und führt die Installation im Hintergrund durch.

__Hinweis: Im Moment lassen sich mehrere Pakete nur dann gleichzeitig installieren, wenn sich diese auf der selben Ergebnisseite befinden.__ 

### Install Tool aufrufen
Der Contao Manager kann in der aktuellen Version nicht auf die Datenbank zugreifen.

Aus diesem Grund müssen Sie nach jeder Installation auf den Button *Install Tool* klicken und die Datenbank manuell aktualisieren.


## Pakete deinstallieren
Wenn Sie eine Extension nicht mehr benötigen, klicken Sie in der Übersicht auf die Schaltfläche *Remove* und anschießend auf *Apply changes*.
Es wird wieder ein Task im Hintergrund ausgeführt. Anschließend müssen Sie wieder das Install Tool aufrufen und die Datenbank aktualisieren.

Bitte beachten Sie, dass die Contao-Core-bundles ebenfalls in der Liste stehen und theoretisch deinstalliert werden könnten.
