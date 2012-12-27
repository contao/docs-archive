# Seiten verwalten

Die folgenden Kapitel erklären, wie man Seiten in Contao verwaltet. Da Contao
ein Seiten-basiertes CMS ist, sind Seiten und die Seitenstruktur die zentralen
Elemente Ihrer Webseite und jeder Inhalt, der nicht mit einer Seite assoziiert
ist, erscheint auch niemals im Frontend.


## Komponenten

Das Zusammenspiel von Seiten, Artikeln, Inhaltselementen und Modulen zu
verstehen, ist der Schlüssel zum Erlernen von Contao. Wie bereits erwähnt, ist
die Seitenstruktur das zentrale Element der Webseite. Besucher rufen
grundsätzlich immer Seiten auf und niemals einzelne Artikel, wie es in einem
Node-basierten Content Management System der Fall ist.

![](https://raw.github.com/contao/docs/2.11/book/de/images/komponenten.jpg)

Das Diagramm verdeutlicht, dass Artikel und Layouts die beiden wichtigsten
Komponenten einer Seite sind. Während Artikel die Inhalte einer Seite
speichern, legt das Seitenlayout fest, wie diese auf der Webseite dargestellt
werden. Layouts in Contao sind natürlich CSS-basiert und verwenden keine
Layout-Tabellen. Auf den folgenden Seiten wird erklärt, wie man Stylesheets und
Frontend-Module anlegt, sie zu einem Layout kombiniert und sie anschließend
einer neu erstellten Seite zuweist.


## Themes

Obwohl der Theme-Manager eine neue Funktion der Version 2.9 ist, handelt es sich
dabei eigentlich nur um ein erweitertes Interface für etwas, das es in Contao
schon immer gegeben hat. Das Design einer Webseite besteht normalerweise aus
Stylesheets, Frontendmodulen, Seitenlayouts, Dateien und Templates, die Sie im
Contao-Backend verwalten können. Der Theme-Manager ändert diesen Ansatz nicht,
er fügt lediglich eine Möglichkeit hinzu, die Ressourcen zu exportieren und
wieder zu importieren ([Video-Einführung ansehen][1]).


### Themes versus Frontend-Templates

Der Hauptunterschied zwischen Themes und [Frontend-Templates][2] ist, dass ein
Frontend-Template eine vollständig vorkonfigurierte Beispielwebseite mit einer
beispielhaften Seitenstruktur, Artikeln, Inhaltselementen und sogar Benutzern
und Gruppen enthält. Ein Theme enthält dagegen nur das eigentliche Design der
Webseite und kann deswegen importiert werden, ohne dass bestehende Daten
verloren gehen.

![](https://raw.github.com/contao/docs/2.11/book/de/images/themes-verwalten.jpg)


### Theme-Bestandteile

Ein Theme ist eine Gruppe von [Stylesheets][3], [Frontend-Modulen][4] und
[Seitenlayouts][5], die alle in der Datenbank gespeichert sind und automatisch
vom Theme Exporter erkannt werden. Sie werden diese Elemente in den nächsten
Abschnitten näher kennenlernen. Ein Theme beinhaltet darüber hinaus meistens
auch Bilder und andere Dateien aus dem Files-Verzeichnis sowie optional
angepasste Templates aus dem Templates-Verzeichnis. Diese Ressourcen sind jedoch
nicht automatisch mit dem Theme verlinkt und müssen deswegen in den
Theme-Einstellungen hinzugefügt werden, damit sie beim Theme-Export
berücksichtigt werden.

![](https://raw.github.com/contao/docs/2.11/book/de/images/theme-einstellungen.jpg)


### Theme-Export und Import

Um ein Theme zu exportieren, klicken Sie einfach auf die Export-Schaltfläche
und speichern Sie die .cto-Datei auf Ihrem lokalen Computer. Obwohl .cto eine
proprietäre Dateiendung für Contao-Themes ist, handelt es sich dabei
eigentlich um ZIP-Archive, die Sie mit jedem Programm entpacken können, das
.zip-Dateien unterstützt. Um ein Theme zu reimportieren, übertragen Sie die
.cto-Datei auf Ihren Webserver, öffenen Sie den Theme-Manager im Contao-Backend
und klicken Sie auf "Theme importieren". Sie können mehrere Themes auf einmal
importieren. Nachdem der Import abgeschlossen ist, können Sie das Seitenlayout
des neuen Theme in der Seitenstruktur zuweisen.


## Stylesheets

Barrierefreie Webseiten sollten immer mit CSS formatiert werden, daher enthält
Contao ein "Stylesheets"-Modul, mit dem Sie Formatdefinitionen bequem im Backend
verwalten können. Um die verschiedenen Contao-Elemente und -Module in einem
Stylesheet zu referenzieren, müssen Sie deren Klassennamen kennen.
[Inhaltselement-Klassen][6] beginnen mit "ce_" (z.B. "ce_text") und
[Modul-Klassen][7] mit "mod_" (z.B. "mod_search"). Falls Sie sich nicht sicher
sind, sehen Sie einfach im Quelltext der Webseite nach.

![](https://raw.github.com/contao/docs/2.11/book/de/images/stylesheet.jpg)

Jedes Stylesheet kann auf einen oder mehrere Medientypen und/oder eine bestimmte
Version des Internet Explorers beschränkt werden, falls Sie einen der vielen
darin enthaltenen Fehler gesondert beheben müssen. Achten Sie dabei auf die
Reihenfolge der Formatdefinitionen, da frühere Anweisungen von späteren
überschrieben werden können.

``` {.css}
/* Zuerst den generellen Abstand setzen */
.mod_search {
    margin:24px;
}

/* Danach die spezielle IE7-Anweisung */
*:first-child+html .mod_search {
    margin:18px;
}
```

Wäre die Reihenfolge umgekehrt, würde der allgemeine Abstand den
IE-spezifischen Wert überschreiben.


## Module

Mit Hilfe von Frontend-Modulen können Sie Ihre Webseite um fast jedeerdenkliche
Funktionalität erweitern. Der Contao-Core enthältModule, um verschiedene
Navigationsmodule zu erstellen, dieBenutzerregistrierung und -anmeldung zu
ermöglichen, die Webseite zudurchsuchen, RSS-Feeds zu importieren und vieles
mehr. Module können imBackend unter "Themes" -> "Frontend-Module" konfiguriert
werden.

<table>
<tr>
  <th>Modul</th>
  <th>CSS-Klasse</th>
  <th>Beschreibung</th>
</tr>
<tr>
  <td>Navigationsmenü</td>
  <td>mod_navigation</td>
  <td>Erzeugt ein Navigationsmenü aus der Seitenstruktur.</td>
</tr>
<tr>
  <td>Individuelle Navigation</td>
  <td>mod_customnav</td>
  <td>Erzeugt ein individuelles Navigationsmenü.</td>
</tr>
<tr>
  <td>Navigationspfad</td>
  <td>mod_breadcrumb</td>
  <td>Erzeugt einen Navigationspfad (Breadcrumb).</td>
</tr>
<tr>
  <td>Quicknavigation</td>
  <td>mod_quicknav</td>
  <td>Erzeugt ein Drop-Down-Menü aus der Seitenstruktur.</td>
</tr>
<tr>
  <td>Quicklink</td>
  <td>mod_quicklink</td>
  <td>Erzeugt ein individuelles Drop-Down-Menü.</td>
</tr>
<tr>
  <td>Buchnavigation</td>
  <td>mod_booknav</td>
  <td>Erzeugt ein Buchnavigationsmenü.</td>
</tr>
<tr>
  <td>Artikelnavigation</td>
  <td>mod_article_nav</td>
  <td>Erzeugt ein Seitenumbruch-Menü zur Artikelnavigation.</td>
</tr>
<tr>
  <td>Sitemap</td>
  <td>mod_sitemap</td>
  <td>Erzeugt eine Liste aller Seiten aus der Seitenstruktur.</td>
</tr>
<tr>
  <td>Login-Formular</td>
  <td>mod_login</td>
  <td>Erzeugt ein Anmeldeformular (Login).</td>
</tr>
<tr>
  <td>Automatischer Logout</td>
  <td>-</td>
  <td>Meldet einen Benutzer automatisch ab (Logout).</td>
</tr>
<tr>
  <td>Persönliche Daten</td>
  <td>member_default</td>
  <td>Erzeugt ein Formular zur Bearbeitung der Benutzerdaten.</td>
</tr>
<tr>
  <td>Registrierung</td>
  <td>member_default</td>
  <td>Erzeugt ein Formular zur Benutzerregistrierung.</td>
</tr>
<tr>
  <td>Passwort vergessen</td>
  <td>mod_password</td>
  <td>Erzeugt ein Formular Passwort-Anforderung.</td>
</tr>
<tr>
  <td>Formular</td>
  <td>mod_form</td>
  <td>Fügt der Seite ein Formular hinzu.</td>
</tr>
<tr>
  <td>Suchmaschine</td>
  <td>mod_search</td>
  <td>Fügt der Seite ein Suchfomular hinzu.</td>
</tr>
<tr>
  <td>Artikelliste</td>
  <td>mod_article_list</td>
  <td>Erzeugt eine Liste aller Artikel einer Spalte.</td>
</tr>
<tr>
  <td>Eigener HTML-Code</td>
  <td>-</td>
  <td>Erlaubt das Hinzufügen von eigenem HTML-Code.</td>
</tr>
<tr>
  <td>Flash-Film</td>
  <td>mod_flash</td>
  <td>Bindet einen Flash-Film in eine Seite ein.</td>
</tr>
<tr>
  <td>Zufallsbild</td>
  <td>mod_random_image</td>
  <td>Fügt der Seite ein zufällig ausgewähltes Bild hinzu.</td>
</tr>
<tr>
  <td>Auflistung</td>
  <td>list_default</td>
  <td>Listet die Daten einer beliebigen Tabelle auf.</td>
</tr>
<tr>
  <td>RSS-Reader</td>
  <td>rss_default</td>
  <td>Fügt der Seite einen RSS-Feed hinzu.</td>
</tr>
</table>


### Zugriffsschutz

Jedes Frontend-Modul kann geschützt werden, so dass es nur Gäste oder Benutzer
einer bestimmten Mitgliedergruppe sehen können.

![](https://raw.github.com/contao/docs/2.11/book/de/images/geschuetztes-modul.jpg)


## Seitenlayouts

Seitenlayouts definieren den grundsätzlichen Aufbau einer Seite, wie z.B. die
Anzahl der Spalten oder die Gesamtbreite, und sie legen fest, welche
Frontend-Module in welcher Spalte angezeigt werden. Sie ermöglichen zudem das
Einbinden von Stylesheets und RSS- bzw. Atom-Feeds sowie das Einfügen einer
Google Analytics ID oder beliebigem JavaScript-Code, der für die Steuerung
interaktiver Elemente und Plugins benötigt wird. Das Contao CSS-Framework teilt
das Browserfenster automatisch in mehrere Layoutbreiche auf.

![](https://raw.github.com/contao/docs/2.11/book/de/images/front-end-structure.jpg)

![](https://raw.github.com/contao/docs/2.11/book/de/images/frontend-module.jpg)

Das impliziert, dass Sie zum Zeitpunkt der Erstellung eines Seitenlayouts
bereits die benötigten Stylesheets und Frondend-Module angelegt haben müssen.
Daher wird folgende Reihenfolge beim Anlegen von Ressourcen empfohlen:

* Erstellen der benötigten Stylesheets
* Erstellen der benötigten Frontend-Module
* Optionale Erstellung von Nachrichtenarchiven oder Kalendern
* Erstellen eines neuen Seitenlayouts und Einbindung der Komponenten


## Seitentypen

Der Typ einer Seite legt fest, ob sie statische Inhalte ausgibt, zu einer
anderen Seite weiterleitet oder den Startpunkt einer Webseite innerhalb der
Seitenstruktur markiert. Contao unterstützt folgende 6 Seitentypen:

<table>
<tr>
  <th>Seitentyp</th>
  <th>Beschreibung</th>
</tr>
<tr>
  <td>Reguläre Seite</td>
  <td>Eine reguläre Seite enthält Artikel und Inhaltselemente. Sie verhält
      sich wie eine statische HTML-Seite.</td>
</tr>
<tr>
  <td>Externe Weiterleitung</td>
  <td>Diese Seite leitet Besucher automatisch zu einer externen Webseite um
      (entspricht einem Hyperlink).</td>
</tr>
<tr>
  <td>Interne Weiterleitung</td>
  <td>Diese Seite leitet Besucher automatisch zu einer anderen Seite innerhalb
      der Seitenstruktur um.</td>
</tr>
<tr>
  <td>Startpunkt einer Webseite</td>
  <td>Diese Seite kennzeichnet den Startpunkt einer neuen Webseite innerhalb der
      Seitenstruktur.</td>
</tr>
<tr>
  <td>403 Zugriff verweigert</td>
  <td>Beim Aufruf einer geschützte Seite ohne Zugriffsrechte wird stattdessen
      die 403-Fehlerseite geladen.</td>
</tr>
<tr>
  <td>404 Seite nicht gefunden</td>
  <td>Beim Aufruf einer nicht vorhandenen Seite wird stattdessen die
      404-Fehlerseite geladen.</td>
</tr>
</table>


### Multidomain-Betrieb

Contao unterstützt mehrere Webseiten innerhalb der Seitenstruktur und leitet
Besucher je nach DNS- und Spracheinstellungen automatisch auf einen bestimmten
Startpunkt einer Webseite weiter. Nehmen wir an, Sie betreiben eine
zweisprachige Firmenwebseite unter "www.firma.de" und eine kleine private
Webseite unter der Domain "www.private-seite.de". Sie benötigen dafür drei
Startpunkte:

<table>
<tr>
  <th>Typ</th>
  <th>DNS</th>
  <th>Sprachenkürzel</th>
  <th>Fallback-Sprache</th>
</tr>
<tr>
  <td>Deutsche Firmenseite</td>
  <td>keine</td>
  <td>de</td>
  <td>nein</td>
</tr>
<tr>
  <td>Englische Firmenseite</td>
  <td>keine</td>
  <td>en</td>
  <td>ja</td>
</tr>
<tr>
  <td>Private Webseite</td>
  <td>private-seite.de</td>
  <td>de</td>
  <td>ja</td>
</tr>
</table>

Die folgende Tabelle zeigt, zu welcher Seite ein Besucher abhängig von der
Domain und seiner Browsersprache weitergeleitet wird.

<table>
<tr>
  <th>Domain</th>
  <th>Browsersprache</th>
  <th>Weiterleitung</th>
</tr>
<tr>
  <td>www.firma.de</td>
  <td>Englisch</td>
  <td>Englische Firmenseite</td>
</tr>
<tr>
  <td>www.firma.de</td>
  <td>Deutsch</td>
  <td>Deutsche Firmenseite</td>
</tr>
<tr>
  <td>www.firma.de</td>
  <td>Spanisch</td>
  <td>Englische Firmenseite</td>
</tr>
<tr>
  <td>www.private-seite.de</td>
  <td>egal</td>
  <td>Persönliche Webseite</td>
</tr>
</table>

Beachten Sie, dass die persönliche Webseite ohne die Option "Sprachen-Fallback"
nur für deutsche Benutzer sichtbar wäre!


### Zugriffsrechte

Zugriffsrechte legen fest, was Backend-Benutzer mit einer Seite und ihren
Artikeln machen dürfen. Sie haben nichts mit dem Zugriffsschutz zu tun, der den
Zugriff auf eine Seite im Frontend limitiert! Ähnlich dem Unix-Rechtesystem
gibt es drei Zugriffsebenen:

* Zugriff als Besitzer einer Seite
* Zugriff als Mitglied der Gruppe einer Seite
* Zugriff als unpriviligierter Benutzer


Für jede Zugriffsebene können gesonderte Rechte vergeben werden.
Standardmäßig darf der Besitzer einer Seite sowohl die Seite selbst, als auch
die damit verbundenen Artikel bearbeiten. Ein Mitglied der Gruppe einer Seite
darf hingegen nur die Artikel bearbeiten und ein unpriviligierter Benutzer hat
überhaupt keine Schreibrechte.

![](https://raw.github.com/contao/docs/2.11/book/de/images/benutzerrechte.jpg)


[1]: http://www.youtube.com/watch?v=6z744hsR8I0
[2]: https://contao.org/de/contao-themes-and-templates.html
[3]: 03-Seiten-verwalten.md#stylesheets
[4]: https://contao.org/de/modules.html
[5]: https://contao.org/de/page-layouts.html
[6]: https://contao.org/de/articles.html
[7]: https://contao.org/de/modules.html
