# Systemadministration

Die folgenden Kapitel erklären, wie man Contao administriert. Nebender
Installation und Aktualisierung des Systems ist der Administratorauch für das
Anlegen von Benutzern und Gruppen, dieErweiterungsverwaltung und die Wartung der
Applikation zuständig.


## Benutzer und Gruppen

Contao unterscheidet zwischen Backend-Benutzern ("Benutzer"), die sich am
Administrationsbereich anmelden können, und Frontend-Benutzern
("Mitglieder"),die sich auf der Webseite anmelden können. Im Gegensatz
zuAdministratoren, die standardmäßig alle Seiten und Elemente
bearbeitendürfen ("allow all"), können reguläre Benutzer nur auf
dieRessourcen zugreifen, die explizit in ihrem Profil oder dem Profileiner der
Gruppen, denen sie angehören, freigeschaltet wurden ("deny all").


### Benutzer

Jeder Benutzer kann mehreren Gruppen angehören und erbt automatisch deren
Rechte. Zugriffsrechte sind additiv, das heißt ein Benutzer erbt die Summe der
Rechte aller seiner Gruppen. Wird ein bestimmtes Recht in Gruppe A vergeben,
kann es nicht in Gruppe B widerrufen werden.


#### Pagemounts

Pagemounts legen fest, welche Seiten ein Benutzer in der Seitenstruktur sehen
kann. Der nachfolgende Screenshot zeigt die Seitenstruktur aus Sicht von Helen
Lewis. Obwohl die Webseite wesentlich mehr Seiten enthält, kann sie nur drei
davon sehen, denn nur die "Courses"-Seite wurde in in der "Editors"-Gruppe
gemountet. Beachten Sie außerdem, dass Helen Lewis nur eine der drei Seiten
bearbeiten kann!

![](https://raw.github.com/contao/docs/3.1/manual/de/images/seitenstruktur-hlewis.jpg)

Eine Seite sehen zu können beinhaltet noch nicht das Recht, sie zu bearbeiten.
Erinnern Sie sich, dass [Zugriffsrechte][1] in der Seitenstruktur vergeben
werden, daher muss eine Seite sowohl im Benutzerprofil gemountet, als auch in
der Seitenstruktur freigeschaltet werden.


#### Filemounts

Filemounts legen fest, welche Verzeichnisse ein Benutzer in der Dateiverwaltung
sehen kann. Der nachfolgende Screenshot zeigt den Dateimanager aus Sicht von
Helen Lewis, die im Gegensatz zum Administrator nur auf den `campus`-Ordner
zugreifen darf.

![](https://raw.github.com/contao/docs/3.1/manual/de/images/dateiverwaltung-hlewis.jpg)


#### Erlaubte Felder

Wie oben erwähnt, haben reguläre Benutzer standardmäßig überhaupt keine
Rechte ("deny all"), dürfen also auch nicht auf Formularfelder zugreifen.
Selbst wenn sie also beispielsweise das Nachrichten-Modul aufrufen könnten,
wäre das Formular zum Anlegen eines Beitrags solange leer, bis der
Administrator in den Gruppenrechten eines oder mehrere Felder der Tabelle
`tl_news` freigeschaltet hat.

![](https://raw.github.com/contao/docs/3.1/manual/de/images/erlaubte-felder.jpg)


### Mitglieder

Die Verwaltung von Mitgliedern (Frontend-Benutzern) ist viel simpler als die von
Backend-Benutzern, weil es keine Pagemounts oder erlaubte Felder gibt. Die
Mitgliederverwaltung wird hauptsächlich benötigt, um den auf Gruppenebene
implementierten Zugriffsschutz für Seiten zu kontrollieren. Je nach
Konfiguration können registrierte Mitglieder geschützte Seiten oder Downloads
aufrufen, die für Gäste nicht erreichbar sind.


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

![](https://raw.github.com/contao/docs/3.1/manual/de/images/erweiterungsliste.jpg)

Die Detailseite enthält die Beschreibung der Erweiterung sowie wichtige
Informationen zu Systemvoraussetzungen, Versionen und Abhängigkeiten von
anderen Modulen. Klicken Sie auf die "Installieren"-Schaltfläche, um die
Erweiterung herunterzuladen und zu installieren.

![](https://raw.github.com/contao/docs/3.1/manual/de/images/erweiterungsdetails.jpg)

Contao lädt die Erweiterung automatisch herunter, kopiert die Dateien und
aktualisiert wenn nötig die Datenbank.

![](https://raw.github.com/contao/docs/3.1/manual/de/images/erweiterung-installieren.jpg)


### Erweiterungsverwaltung

Mit dem Modul "Erweiterungsverwaltung" können Erweiterungen aktualisiert oder
deinstalliert werden. Es wird automatisch auf Updates geprüft und auf neue
Versionen hingewiesen. Viele Erweiterungen enthalten außerdem einen
Support-Link zur Dokumentation und/oder zum Forum.

![](https://raw.github.com/contao/docs/3.1/manual/de/images/erweiterungsverwaltung.jpg)

Um eine Erweiterung zu deinstallieren, klicken Sie auf das entsprechende Icon
und folgen Sie den Anweisungen. Es werden alle Dateien entfernt und falls nötig
die Datenbank aktualisiert. Beachten Sie, dass diese Aktion nicht rückgängig
gemacht werden kann!

![](https://raw.github.com/contao/docs/3.1/manual/de/images/erweiterung-deinstallieren.jpg)


### Manuelle Installation

Falls die PHP SOAP-Erweiterung auf Ihrem Server nicht verfügbar ist, können
Sie Extensions auch manuell installieren. Finden Sie das entsprechende Modul in
der [Erweiterungsliste][2] und laden Sie das .zip-Archiv des aktuellen Release
herunter. Entpacken Sie die Dateien und kopieren Sie sie in Ihr lokales oder
entferntes Contao-Verzeichnis. Abschließend prüfen Sie die Datenbank mit dem
[Contao-Installtool][3].


## Systemwartung

Die meisten Wartungsaufgaben in Contao sind automatisiert, so dass Sie sich auf
Ihre eigentliche Arbeit konzentrieren können. Manchmal kann es jedoch notwendig
sein, die sonst automatisch ausgeführten Aufgaben der Systemwartung manuell zu
starten.


### Daten bereinigen

Neben den Benutzer-generierten Inhalten speichert Contao verschiedene
Systemdaten, die für die Suche oder das Wiederherstellen gelöschter
Datensätze oder früherer Versionen verwendet werden. Sie können diese Daten
manuell bereinigen, um z.B. alte Vorschaubilder zu entfernen oder die
XML-Sitemaps nach einer Änderung an der Seitenstruktur zu aktualisieren.

![](https://raw.github.com/contao/docs/3.1/manual/de/images/daten-bereinigen.jpg)


### Suchindex neu aufbauen

Seiten werden automatisch beim Aufruf im Frontend indiziert (es sei denn Sie
sind parallel im Backend angemeldet), daher müssen Sie sich um den Suchindex
normalerweise keine Gedanken machen. Wenn Sie allerdings viele Seiten auf einmal
aktualisiert haben, ist es bequemer, den Suchindex manuell neu aufzubauen, als
alle geänderten Seiten einzeln im Browser aufzurufen.

![](https://raw.github.com/contao/docs/3.1/manual/de/images/suchindex-neu-aufbauen.jpg)


[1]: 03-Managing-pages.md#zugriffsschutz
[2]: https://contao.org/de/extension-list.html
[3]: 01-Installation.md#das-contao-installtool
