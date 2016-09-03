## Seitenlayouts

Seitenlayouts definieren den grundsätzlichen Aufbau einer Seite, wie z.B. die
Anzahl der Spalten oder die Gesamtbreite, und sie legen fest, welche
[Frontend-Module][1] in welcher Spalte angezeigt werden. Sie ermöglichen zudem
das Einbinden von Stylesheets und RSS- bzw. Atom-Feeds sowie das Einfügen einer
Google Analytics ID oder beliebigem JavaScript-Code, der für die Steuerung
interaktiver Elemente und Plugins benötigt wird. Das Contao CSS-Framework teilt
das Browserfenster automatisch in mehrere Layoutbereiche auf.

Das Beispiel unten zeigt eine Seite mit vier Layoutbereichen:

1. einem Header (`#header`)
2. einer Sidebar (`#left`)
3. dem Hauptbereich (`#main`)
4. einem Footer (`#footer`)

![](images/front-end-structure.jpg)

Die Module werden entsprechend der Konfiguration im Seitenlayouts in den
entsprechenden Layoutbereichen ausgegeben:

![](images/frontend-module.jpg)

Das impliziert, dass Sie zum Zeitpunkt der Erstellung eines Seitenlayouts
bereits die benötigten Stylesheets und Frondend-Module angelegt haben müssen.
Daher wird folgende Reihenfolge beim Anlegen von Ressourcen empfohlen:

* Erstellen der benötigten Stylesheets
* Erstellen der benötigten Frontend-Module
* Optionale Erstellung von Nachrichtenarchiven oder Kalendern
* Erstellen eines neuen Seitenlayouts und Einbindung der Komponenten


[1]: ../03-seiten-verwalten/module.md
