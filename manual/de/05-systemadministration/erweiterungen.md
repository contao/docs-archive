## Erweiterungen

Erweiterungen sind ein wichtiger Bestandteil von Contao, weil sie das
Hinzufügen weiterer Funktionalität ermöglichen. Momentan befinden sich 1.400
Erweiterungen im Extension Repository, die Sie direkt im Backend aufrufen
können. Beachten Sie dabei, dass das Extension Repository 2.0 nur noch solche
Erweiterungen anzeigt, die zu Ihrer Contao-Version kompatibel sind. Die Anzahl
der Erweiterungen in Ihrem Erweiterungskatalog wird daher je nach Version
wahrscheinlich deutlich unter 1.400 liegen. Die Kommunikation mit dem
Repository-Server erfolgt mittels SOAP, daher benötigen Sie die PHP
SOAP-Erweiterungen, um den Service zu nutzen.


### Erweiterungskatalog

Mit dem "Erweiterungskatalog"-Modul können Sie die Erweiterungsliste
durchsuchen und Erweiterungen auf Knopfdruck installieren. Nutzen Sie die
Filter- und Sortieroptionen zum Auffinden eines Moduls und klicken Sie auf
dessen Namen, um die Beschreibung zu lesen oder es zu installieren.

![](images/erweiterungsliste.jpg?raw=true)

Die Detailseite enthält die Beschreibung der Erweiterung sowie wichtige
Informationen zu Systemvoraussetzungen, Versionen und Abhängigkeiten von
anderen Modulen. Klicken Sie auf die "Installieren"-Schaltfläche, um die
Erweiterung herunterzuladen und zu installieren.

![](images/erweiterungsdetails.jpg?raw=true)

Contao lädt die Erweiterung automatisch herunter, kopiert die Dateien und
aktualisiert wenn nötig die Datenbank.

![](images/erweiterung-installieren.jpg?raw=true)


### Erweiterungsverwaltung

Mit dem Modul "Erweiterungsverwaltung" können Erweiterungen aktualisiert oder
deinstalliert werden. Es wird automatisch auf Updates geprüft und auf neue
Versionen hingewiesen. Viele Erweiterungen enthalten außerdem einen
Support-Link zur Dokumentation und/oder zum Forum.

![](images/erweiterungsverwaltung.jpg?raw=true)

Um eine Erweiterung zu deinstallieren, klicken Sie auf das entsprechende Icon
und folgen Sie den Anweisungen. Es werden alle Dateien entfernt und falls nötig
die Datenbank aktualisiert. Beachten Sie, dass diese Aktion nicht rückgängig
gemacht werden kann!

![](images/erweiterung-deinstallieren.jpg?raw=true)


### Manuelle Installation

Falls die PHP SOAP-Erweiterung auf Ihrem Server nicht verfügbar ist, können
Sie Extensions auch manuell installieren. Finden Sie das entsprechende Modul in
der [Erweiterungsliste][2] und laden Sie das .zip-Archiv des aktuellen Release
herunter. Entpacken Sie die Dateien und kopieren Sie sie in Ihr lokales oder
entferntes Contao-Verzeichnis. Abschließend prüfen Sie die Datenbank mit dem
[Contao-Installtool][3].


[2]: https://contao.org/de/extension-list.html
[3]: 01-Installation.md#das-contao-installtool