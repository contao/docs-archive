# Inhalte verwalten

Die folgenden Kapitel erklären, wie man Inhalte in Contao verwaltet. Der
Contao-Core beinhaltet bereits die grundlegenden Inhaltstypen wie z.B. Artikel,
Nachrichten, Events, Newsletter oder Formatdefinitionen. Weitere Inhaltstypen
wie Banner, Tickets, Produkte oder Empfehlungen sind über das [Extension
Repository][1] verfügbar. Inhalte können im Backend mit den entsprechenden
Modulen angelegt werden.


## Artikel

Artikel sind Container für Inhaltselemente. Das Gruppieren zusammengehöriger
Inhaltselemente macht es einfach, sie alle auf einmal zu verschieben, zu
veröffentlichen, zu kopieren oder zu exportieren, anstatt jedes einzelne
Element zu bearbeiten. Jeder Artikel ist mit einer bestimmten Seite und einem
Layoutbereich assoziiert und hat daher eine feste Position innerhalb der
Seitenstruktur und auf der Webseite.


### Inhaltselemente

Inhaltselemente sind ein einfacher und intuitiver Weg, um Inhalte zuerstellen.
Anstatt nur den Rich Text Editor zu verwenden, bietet Contao für jeden
Inhaltstyp wie z.B. Texte, Listen, Tabellen, Hyperlinks, Bilder oder Downloads
ein eigenes Element. Nachfolgend finden Sie eine Übersicht über die im
Contao-Core enthaltenen Inhaltselemente.

<table>
<tr>
  <th>Name</th>
  <th>CSS-Klasse</th>
  <th>Beschreibung</th>
</tr>
<tr>
  <td>Überschrift</td>
  <td>ce_headline</td>
  <td>Erzeugt eine Überschrift (h1 - h6).</td>
</tr>
<tr>
  <td>Text</td>
  <td>ce_text</td>
  <td>Erzeugt einen Rich Text, der mit <a href="http://www.tinymce.com">TinyMCE</a>
      formatiert werden kann.</td>
</tr>
<tr>
  <td>HTML</td>
  <td>-</td>
  <td>Erlaubt das Hinzufügen von eigenem HTML-Code.</td>
</tr>
<tr>
  <td>Aufzählung</td>
  <td>ce_list</td>
  <td>Erzeugt eine geordnete oder ungeordnete Liste.</td>
</tr>
<tr>
  <td>Tabelle</td>
  <td>ce_table</td>
  <td>Erzeugt eine optional sortierbare Tabelle.</td>
</tr>
<tr>
  <td>Code</td>
  <td>ce_code</td>
  <td>Gibt formatierten Programmcode auf dem Bildschirm aus.</td>
</tr>
<tr>
  <td>Akkordeon (Einzelelement)</td>
  <td>ce_accordion</td>
  <td>Erzeugt ein einzelnes Akkordeon-Element (Mit <a href="http://mootools.net">MooTools</a>).</td>
</tr>
<tr>
  <td>Akkordeon (Umschlag Anfang)</td>
  <td>ce_accordionStart</td>
  <td>Erzeugt den öffnenden Teil des Akkordeon-Umschlags.</td>
</tr>
<tr>
  <td>Akkordeon (Umschlag Ende)</td>
  <td>-</td>
  <td>Erzeugt den schließenden Teil des Akkordeon-Umschlags.</td>
</tr>
<tr>
  <td>Content-Slider (Umschlag Anfang)</td>
  <td>ce_sliderStart</td>
  <td>Erzeugt den öffnenden Teil des Slider-Umschlags.</td>
</tr>
<tr>
  <td>Content-Slider (Umschlag Ende)</td>
  <td>-</td>
  <td>Erzeugt den schließenden Teil des Slider-Umschlags.</td>
</tr>
<tr>
  <td>Hyperlink</td>
  <td>ce_hyperlink</td>
  <td>Erzeugt einen Verweis auf eine andere Webseite.</td>
</tr>
<tr>
  <td>Top-Link</td>
  <td>ce_toplink</td>
  <td>Erzeugt einen Link zum Seitenanfang.</td>
</tr>
<tr>
  <td>Bild</td>
  <td>ce_image</td>
  <td>Erzeugt ein einzelnes Bild.</td>
</tr>
<tr>
  <td>Galerie</td>
  <td>ce_gallery</td>
  <td>Erzeugt eine <a href="http://www.digitalia.be/software/slimbox">lightbox</a>
      Bildergalerie.</td>
</tr>
<tr>
  <td>Video/Audio</td>
  <td>ce_player</td>
  <td>Erzeugt einen Video- bzw. Audio-Player.</td>
</tr>
<tr>
  <td>YouTube</td>
  <td>ce_youtube</td>
  <td>Fügt ein YouTube-Video ein.</td>
</tr>
<tr>
  <td>Download</td>
  <td>ce_download</td>
  <td>Erzeugt einen Link zum Download einer Datei.</td>
</tr>
<tr>
  <td>Downloads</td>
  <td>ce_downloads</td>
  <td>Erzeugt mehrere Links zum Download von Dateien.</td>
</tr>
<tr>
  <td>Artikel</td>
  <td>-</td>
  <td>Fügt einen anderen Artikel ein.</td>
</tr>
<tr>
  <td>Inhaltselement</td>
  <td>(parent class)</td>
  <td>Fügt ein anderes Inhaltselement ein.</td>
</tr>
<tr>
  <td>Formular</td>
  <td>ce_form</td>
  <td>Fügt ein Formular ein.</td>
</tr>
<tr>
  <td>Modul</td>
  <td>(parent class)</td>
  <td>Fügt ein Frontend-Modul ein.</td>
</tr>
<tr>
  <td>Artikelteaser</td>
  <td>ce_teaser</td>
  <td>Zeigt den Teasertext eines Artikels an.</td>
</tr>
<tr>
  <td>Kommentare</td>
  <td>ce_comments</td>
  <td>Fügt ein Kommentar-Formular ein.</td>
</tr>
</table>


### Zugriffsschutz

Jedes Inhaltselement kann geschützt werden, so dass es nur Gäste oder Benutzer
einer bestimmten Mitgliedergruppe sehen können.

![](images/geschuetztes-element.jpg?raw=true)


### Flash-Inhalte

Flash-Inhalte sind spezielle Inhalte, die nicht als Artikel auf der Webseite
ausgegeben, sondern mittels `loadVars()` in einen dynamischen Flash-Film geladen
werden. Fügen Sie folgendes Skript in Ihren Flash-Film ein, um die Kommunikation
mit Contao zu ermöglichen:

``` {.as}
TextField.prototype._loadArticle = function(flashID) {
  tf = this;

  // HTML-Mode aktivieren
  tf.html = true;
  tf.htmlText = "";

  // LoadVars-Objekt instantiieren
  lv = new LoadVars();
  lv["flashID"] = flashID;
  lv.sendAndLoad(URL + "flash.php", lv, "POST");

  lv.onLoad = function(success) {
    if (success) {
      tf.htmlText = lv["content"];
    }
  }
}

// Den Flash-Inhalt "myArticle" in das Textfeld "myTextBox" laden
myTextBox._loadArticle("myArticle");
```


#### Ein Stylesheet importieren

Das folgende ActionScript erlaubt das Importieren eines Stylesheets zur
Formatierung des Textfeldes:

``` {.as}
TextField.prototype._addCSS = function(style_sheet) {
  tf= this;
  tf.styleSheet = null;

  // StyleSheet-Objekt instantiieren
  st = new TextField.StyleSheet();
  st.load(URL + style_sheet);

  st.onLoad = function(success) {
    if (success) {
      tf.styleSheet = st;
    }
  }
}

// Das Stylesheet "basic.css" zum Textfeld "myTextBox" hinzufügen
myTextBox._addCSS("basic.css");
```

Beachten Sie, dass Flash nur einen kleinen Teil der HTML-Tags unterstützt und
manche Formatierungen daher nicht angezeigt werden können.


## Nachrichten

Die News/Blog-Erweiterung ermöglicht die Verwaltung von Nachrichten bzw.
Blog-Einträgen und deren Darstellung im Frontend. Im Gegensatz zu Artikeln, die
mit einer bestimmten Seite assoziiert sind, werden Nachrichten in Archiven
organisiert und können so einfach gruppiert, kategorisiert oder als RSS- bzw.
Atom-Feed exportiert werden.


### Nachrichtenarchive

Archive werden zur Gruppierung und/oder Kategorisierung von Nachrichten
verwendet. Jedes Archiv kann sich auf eine bestimmte Sprache oder ein bestimmtes
Thema beziehen.


### Frontend-Module

Mit den Frontend-Modulen der News/Blog-Erweiterung können Nachrichten auf der
Webseite dargestellt werden. Module können im Backend unter "Layout" -> "Module"
konfiguriert werden und müssen anschließend in einem Artikel oder Seitenlayout
eingebunden werden.

<table>
<tr>
  <th>Modul</th>
  <th>CSS-Klasse</th>
  <th>Beschreibung</th>
</tr>
<tr>
  <td>Nachrichtenliste</td>
  <td>mod_newslist</td>
  <td>Fügt der Seite eine Nachrichtenliste hinzu.</td>
</tr>
<tr>
  <td>Nachrichtenleser</td>
  <td>mod_newsreader</td>
  <td>Stellt einen einzelnen Nachrichtenbeitrag dar.</td>
</tr>
<tr>
  <td>Nachrichtenarchiv</td>
  <td>mod_newsarchive</td>
  <td>Fügt der Seite ein Nachrichtenarchiv hinzu.</td>
</tr>
<tr>
  <td>Nachrichtenarchiv-Menü</td>
  <td>mod_newsmenu</td>
  <td>Erzeugt ein Menü zur Navigation des Nachrichtenarchivs.</td>
</tr>
</table>


### Permalinks

Jede Nachricht hat eine eindeutige URL (Permalink), die zur Referenzierung des
Beitrags verwendet werden kann:

```
http://www.example.com/news/items/james-wilson-returns.html
```

Die oben genannte URL fordert den Beitrag "james-wilson-returns" auf der Seite
"news" an. Denken sie daran, dass Contao ein Seiten-basiertes CMS ist; gäbe es
die Seite "news" nicht oder enthielte sie nicht das Modul Nachrichtenleser,
würde der Beitrag auch nicht angezeigt.


## Termine

Die Kalender-Erweiterung ermöglicht die Verwaltung von Terminen und deren
Darstellung als Kalender oder Eventliste im Frontend. Im Gegensatz zu Artikeln,
die mit einer bestimmten Seite assoziiert sind, werden Termine in Kalendern
organisiert und können so einfach gruppiert, kategorisiert oder als RSS- bzw.
Atom-Feed exportiert werden.


### Kalender

Kalender werden zur Gruppierung und/oder Kategorisierung von Terminen verwendet.
Jeder Kalender kann sich auf eine bestimmte Sprache oder ein bestimmtes Thema
beziehen.


### Frontend-Module

Mit den Frontend-Modulen der Kalender-Erweiterung können Termine bzw. Events auf
der Webseite dargestellt werden. Module können im Backend unter "Layout" ->
"Module" konfiguriert werden und müssen anschließend in einem Artikel oder
Seitenlayout eingebunden werden.

<table>
<tr>
  <th>Modul</th>
  <th>CSS-Klasse</th>
  <th>Beschreibung</th>
</tr>
<tr>
  <td>Kalender</td>
  <td>mod_calendar</td>
  <td>Fügt der Seite einen Kalender hinzu.</td>
</tr>
<tr>
  <td>Eventleser</td>
  <td>mod_eventreader</td>
  <td>Stellt einen einzelnen Event dar.</td>
</tr>
<tr>
  <td>Eventliste</td>
  <td>mod_eventlist</td>
  <td>Listet alle Events eines bestimmten Zeitraums auf.</td>
</tr>
<tr>
  <td>Eventliste-Menü</td>
  <td>mod_eventmenu</td>
  <td>Erzeugt ein Menü zur Navigation der Eventliste.</td>
</tr>
</table>


### Permalinks

Jeder Termin hat eine eindeutige URL (Permalink), die zur Referenzierung des
Events verwendet werden kann:

```
http://www.example.com/event-reader/events/final-exams.html
```

Die oben genannte URL fordert den Event "final-exams" auf der Seite "events" an.
Denken sie daran, dass Contao ein Seiten-basiertes CMS ist; gäbe es die Seite
"events" nicht oder enthielte sie nicht das Modul Eventleser, würde der Beitrag
auch nicht angezeigt.


## RSS-/Atom-Feed

Diese Funktion ist für News Archive und Kalender verfügbar.
Hier ein Beispiel der Kalender-Liste.

![](images/rss-kalender.jpg?raw=true)


### Einstellungen

Ein oder mehrere Kalender können gruppiert und als RSS- bzw. Atom-Feed
ausgegeben werden. Genau gleich funktioniert es bei News Archiven. Hier kann
auch gewählt werden, ob nur der Teaser oder der komplette Artikel des Events
bzw. der News ausgegeben werden soll.

![](images/rss-bearbeiten.jpg?raw=true)


### XML Dateien

Die XML Dateien werden automatisch generiert und im ```share``` Verzeichnis
Ihrer Contao Installation abgelegt. In diesem Beispiel: ```share/events.xml```.


## Newsletter

Die Newsletter-Erweiterung ermöglicht das Versenden von Newslettern, die
Verwaltung von Abonnements sowie die optionale Ausgabe versendeter Nachrichten
im Frontend. Im Gegensatz zu Artikeln, die mit einer bestimmten Seite assoziiert
sind, werden Newsletter in Verteilern organisiert und können so einfach
gruppiert oder kategorisiert werden.


### Abonnenten

Newsletter-Abonnements werden normalerweise automatisch über die entsprechenden
Frontend-Module verwaltet, ohne dass Sie in den Prozess eingreifen müssten. Aus
datenschutzrechtlichen Gründen muss das Abonnieren eines Verteilers mittels
[Double Opt-In][2] erfolgen und es wird nur die E-Mail-Adresse des Abonnements
gespeichert.

![](images/newsletter-abonnenten.jpg?raw=true)

Falls Sie bereits einen Verteiler haben, können Sie die Abonnenten aus einer
CSV-Datei in Contao importieren.


### Newsletter personalisieren

Insofern Sie Newsletter an registrierte Mitglieder verschicken, können Sie
diese mit Hilfe der sogenannten "Simple Tokens" personalisieren. Simple Tokens
funktionieren ähnlich wie [Inserttags][3] und können sowohl im HTML- als auch
im Text-Inhalt eines Newsletters verwendet werden.

```
Sehr geehrte(r) ##firstname## ##lastname##,

bitte prüfen und aktualisieren Sie Ihre Daten:

Anschrift: ##street##
PLZ/Ort:   ##postal## ##city##
Telefon:   ##phone##
E-Mail:    ##email##

Ihr Administrator
```

Im Gegensatz zu Inserttags können Sie mit Simple Tokens aber nicht nur auf die
Daten der Mitgliedertabelle `tl_member` zugreifen, sondern auch einfache
If-Else-Abfragen realisieren und so beispielsweise die Anrede präzisieren.

```
{if gender=="male"}
Sehr geehrter Herr ##lastname##,
{elseif gender=="female"}
Sehr geehrte Frau ##lastname##,
{else}
Sehr geehrte Damen und Herren,
{endif}

[Inhalt des Newsletters]

{if phone==""}
Bitte aktualisieren Sie Ihre Daten und geben Sie Ihre Telefonnummer an.
{endif}

Ihr Administrator
```


### Newsletter versenden

Speziell auf Shared-Hosting-Servern gibt es normalerweise Limits für die
maximale Skriptlaufzeit und/oder die Anzahl der E-Mails, die pro Minute
versendet werden dürfen. Contao versucht, diese beiden Probleme zu umgehen,
indem der Versendungsprozess in mehreren Teilschritten mit einer bestimmten
Wartezeit dazwischen erfolgt und so die Anzahl der E-Mails pro Minute
kontrolliert werden kann.

![](images/newsletter-versenden.jpg?raw=true)


### Frontend-Module

Mit den Frontend-Modulen der Newsletter-Erweiterung können Abonnements
verwaltet und optional Newsletter angezeigt werden. Module können im Backend
unter "Layout" -> "Module" konfiguriert werden und müssen anschließend in einem
Artikel oder Seitenlayout eingebunden werden.

<table>
<tr>
  <th>Modul</th>
  <th>CSS-Klasse</th>
  <th>Beschreibung</th>
</tr>
<tr>
  <td>Abonnieren</td>
  <td>mod_subscribe</td>
  <td>Erzeugt ein Formular zum Abonnieren von Verteilern.</td>
</tr>
<tr>
  <td>Kündigen</td>
  <td>mod_unsubscribe</td>
  <td>Erzeugt ein Formular zum Kündigen von Abonnements.</td>
</tr>
<tr>
  <td>Newsletterliste</td>
  <td>mod_nl_list</td>
  <td>Fügt der Seite eine Newsletterliste hinzu.</td>
</tr>
<tr>
  <td>Newsletterleser</td>
  <td>mod_nl_reader</td>
  <td>Stellt einen einzelnen Newsletter dar.</td>
</tr>
</table>


### Permalinks

Jeder Newsletter hat eine eindeutige URL (Permalink), die zur Referenzierung der
Nachricht verwendet werden kann:

```
http://www.example.com/newsletters/items/james-wilson-returns.html
```

Die obige URL fordert den Newsletter "james-wilson-returns" auf der Seite
"newsletters" an. Denken sie daran, dass Contao ein Seiten-basiertes CMS ist;
gäbe es die Seite "newsletters" nicht oder enthielte sie nicht das Modul
Newsletterleser, würde der Beitrag auch nicht angezeigt.


## Formulare

Mit dem Formulargenerator lassen sich interaktive Formulare erstellen, die per
E-Mail verschickt oder in der Datenbank gespeichert werden können. Hochgeladene
Dateien werden als Anhang versendet oder auf dem Server gespeichert. Folgende
Datenformate werden unterstützt:

<table>
<tr>
  <th>Format</th>
  <th>Beschreibung</th>
</tr>
<tr>
  <td>Rohdaten</td>
  <td>Die Formulardaten werden als einfache Textnachricht mit einer Zeile pro
      Feld versendet.</td>
</tr>
<tr>
  <td>XML file</td>
  <td>Die Formulardaten werden der E-Mail als XML-Datei angefügt.</td>
</tr>
<tr>
  <td>CSV file</td>
  <td>Die Formulardaten werden der E-Mail als CSV-Datei angefügt.</td>
</tr>
<tr>
  <td>E-mail</td>
  <td>Ignoriert alle Felder außer "email", "subject", "message" und "cc"
      (Carbon Copy) und verschickt die Daten als wären sie mit einem
      E-Mail-Programm versendet worden. Datei-Uploads sind erlaubt.</td>
</tr>
</table>


### Formularfelder

Ähnlich wie bei Inhaltselementen, enthält Contao ein eigenes Element für
jedes Formularfeld, wie z.B. Textfelder, Auswahlmenüs, Dateiuploads, versteckte
Felder oder Schaltflächen. Folgende Formularfelder sind im Contao-Core
enthalten:

<table>
<tr>
  <th>Feld</th>
  <th>CSS-Klasse</th>
  <th>Beschreibung</th>
</tr>
<tr>
  <td>Überschrift</td>
  <td>headline</td>
  <td>Ein individuelles Feld zum Einfügen einer Bereichsüberschrift.</td>
</tr>
<tr>
  <td>Erklärung</td>
  <td>explanation</td>
  <td>Ein individuelles Feld zum Einfügen eines Erklärungstexts.</td>
</tr>
<tr>
  <td>HTML</td>
  <td>-</td>
  <td>Ein individuelles Feld zum Einfügen von HTML-Code.</td>
</tr>
<tr>
  <td>Fieldset</td>
  <td>-</td>
  <td>Ein Container für Formularfelder mit einer optionalen Legende.</td>
</tr>
<tr>
  <td>Textfeld</td>
  <td>text</td>
  <td>Ein einzeiliges Eingabefeld für einen kurzen oder mittellangen Text.</td>
</tr>
<tr>
  <td>Passwortfeld</td>
  <td>password</td>
  <td>Ein einzeiliges Eingabefeld für ein Passwort. Contao fügt automatisch
      ein Bestätigungsfeld hinzu.</td>
</tr>
<tr>
  <td>Textarea</td>
  <td>textarea</td>
  <td>Ein mehrzeiliges Eingabefeld für einen mittellangen oder langen Text.</td>
</tr>
<tr>
  <td>Select-Menü</td>
  <td>select/multiselect</td>
  <td>Ein ein- oder mehrzeiliges Drop-Down-Menü.</td>
</tr>
<tr>
  <td>Radio-Button-Menü</td>
  <td>radio</td>
  <td>Eine Liste mehrerer Optionen, von denen eine ausgewählt werden kann.</td>
</tr>
<tr>
  <td>Checkbox-Menü</td>
  <td>checkbox</td>
  <td>Eine Liste mehrerer Optionen, von denen beliebig viele ausgewählt werden
      können.</td>
</tr>
<tr>
  <td>Datei-Upload</td>
  <td>upload</td>
  <td>Ein einzeiliges Eingabefeld zur Übertragung lokaler Dateien auf den
      Server.</td>
</tr>
<tr>
  <td>Verstecktes Feld</td>
  <td>-</td>
  <td>Ein einzeiliges Eingabefeld, das im Formular nicht sichtbar ist.</td>
</tr>
<tr>
  <td>Sicherheitsfrage</td>
  <td>captcha</td>
  <td>Eine einfache Rechenaufgabe zur Prüfung ob das Formular von einem
      Menschen abgesendet wurde (CAPTCHA).</td>
</tr>
<tr>
  <td>Absendefeld</td>
  <td>submit</td>
  <td>Eine Absende-Schaltfläche zur Versendung des Formulars.</td>
</tr>
</table>


### Frontend-Modul

Mit dem Frontend-Module des Formulargenerators können Formulare angezeigt werden.
Module können im Backend unter "Layout" -> "Module" konfiguriert werden und
müssen anschließend in einem Artikel oder Seitenlayout eingebunden werden.

<table>
<tr>
  <th>Modul</th>
  <th>CSS-Klasse</th>
  <th>Beschreibung</th>
</tr>
<tr>
  <td>Formular</td>
  <td>mod_form</td>
  <td>Fügt ein Formular auf der Seite ein.</td>
</tr>
</table>


### Inhaltselement

Das Inhaltselement bietet dieselben Funktionen wie das Modul, lässt sich aber
direkt im Artikel einbinden und konfigurieren. Der Formulargenerator
stellt ein Inhaltselement zur Verfügung:

<table>
<tr>
  <th>Inhaltselement</th>
  <th>CSS-Klasse</th>
  <th>Beschreibung</th>
</tr>
<tr>
  <td>Formular</td>
  <td>ce_form</td>
  <td>Fügt ein Formular ein.</td>
</tr>
</table>


## Kommentare

Kommentare sind eine weitere Form von Inhalt, welcher über das Backend
verwaltet werden kann. Kommentare können in Kalendern und News-Archiven
aktiviert werden.


### Frontend-Modul

Mit dem Frontend-Module der Kommentar-Erweiterung können Kommentare ein- und
ausgegeben werden. Module können im Backend unter "Layout" -> "Module"
konfiguriert werden und müssen anschließend in einem Artikel oder Seitenlayout
eingebunden werden.

<table>
<tr>
  <th>Modul</th>
  <th>CSS-Klasse</th>
  <th>Beschreibung</th>
</tr>
<tr>
  <td>Kommentare</td>
  <td>mod_comments</td>
  <td>Bietet Kommentare oder eine Gästebuch-Funktion.</td>
</tr>
</table>


### Inhaltselement

Das Inhaltselement bietet dieselben Funktionen wie das Modul, lässt sich aber
direkt im Artikel einbinden und konfigurieren. Die Kommentar-Erweiterung
stellt ein Inhaltselement zur Verfügung:

<table>
<tr>
  <th>Inhaltselement</th>
  <th>CSS-Klasse</th>
  <th>Beschreibung</th>
</tr>
<tr>
  <td>Kommentare</td>
  <td>ce_comments</td>
  <td>Fügt das Kommentar-Formular auf der Seite ein.</td>
</tr>
</table>


### BBCode

Der Besucher kann ausserdem die [BBCode Sprache][7] verwenden.
Contao versteht folgende Tags:

<table>
<tr>
  <th>BBCode</th>
  <th>Beschreibung</th>
</tr>
<tr>
  <td>[b][/b]</td>
  <td>Der enthaltene Text wird fett dargestellt.</td>
</tr>
<tr>
  <td>[i][/i]</td>
  <td>Der enthaltene Text wird kursiv dargestellt.</td>
</tr>
<tr>
  <td>[u][/u]</td>
  <td>Der enthaltene Text wird unterstrichen.</td>
</tr>
<tr>
  <td>[img][/img]</td>
  <td>Ersetzen das Tag durch ein Bild (Bild-Pfad zwischen den Tags).</td>
</tr>
<tr>
  <td>[code][/code]</td>
  <td>Der enthaltene Text wird in einer Schrift mit fester Laufweite
  dargestellt.</td>
</tr>
<tr>
  <td>[color=#ff0000][/color]</td>
  <td>Der enthaltene Text wird in der entsprechenden Farbe dargestellt.</td>
</tr>
<tr>
  <td>[quote][/quote]</td>
  <td>Stellt den entsprechenden Text als Zitat dar.</td>
</tr>
<tr>
  <td>[quote=John]Hallo[/quote]</td>
  <td>Stellt den entsprechenden Text als Zitat eines Autors dar.</td>
</tr>
<tr>
  <td>[url][/url]</td>
  <td>Die enthaltene URL wird als Link dargestellt.</td>
</tr>
<tr>
  <td>[url=http://][/url]</td>
  <td>Der enthaltene Text wird mit der entsprechenden URL verlinkt.</td>
</tr>
<tr>
  <td>[email][/email]</td>
  <td>Die enthaltene E-Mail-Adresse wird als Link dargestellt.</td>
</tr>
<tr>
  <td>[email=name@example.com][/email]</td>
  <td>Der enthaltene Text wird mit der E-Mail-Adresse verknüpft.</td>
</tr>
</table>


## Templates

Ein Template enthält meist HTML und PHP code. Es wird zur Ausgabe von Inhalten 
eines Moduls oder Inhaltelements etc. verwendet. Beispielsweise gibt das 
Template `news_full.html5` eine vollständige Nachricht aus, während das Template 
`news_short.html5` nur einen Teil davon anzeigt.

Templates befinden sich direkt in den dazugehören Modulen. Das `news_full.html5` 
Template befindet sich beispielsweise in `system/modules/news/templates/news`.

Falls diese Datei direkt in diesem Ordner bearbeitet wird, **gehen die Änderungen** 
bei einem nächsten Update von Contao **verloren**. Um dies zu vermeiden, 
Templates können im Backend bearbeitet werden. Dabei wird die Datei kopiert um 
Änderungen während einem Update nicht zu verlieren.

![](images/templates.jpg?raw=true)

Unter dem Menüpunkt *Templates* können die Dateien bearbeitet und in Ordnern 
abgelegt werden. Ordner müssen wie unter [Theme-Bestandteile][8] beschrieben 
einem Theme zugewiesen sein.

Ein Template gehört zu einem Modul, einem Inhaltselement, einem Formular oder 
anderen Komponenten. Sie werden zur einfacheren Erkennung deshalb meist mit 
einem Präfix versehen. Beispielsweise deutet `j_` auf jQuery oder `nl_` auf 
ein Newsletter-Template.


## Inserttags

Inserttags sind Platzhalter, die bei der Ausgabe einer Seite durch bestimmte
Inhalte ersetzt werden. So kann beispielsweise das aktuelle Datum angezeigt oder
ein Benutzer mit seinem Namen angesprochen werden. Inserttags können fast
überall in Contao verwendet werden.


### Link-Elemente

Mit den folgenden Inserttags können Seiten und Artikel anhand ihrer ID oder
ihres Alias verlinkt werden.

{% raw %}
<table>
<tr>
  <th>Insert-Tag</th>
  <th>Beschreibung</th>
</tr>
<tr>
  <td><code>{{link::*}}</code></td>
  <td>Dieses Tag wird mit einem Link zu einer internen Seite ersetzt (ersetzen
      Sie * mit der ID oder dem Alias).</td>
</tr>
<tr>
  <td><code>{{link::back}}</code></td>
  <td>Dieses Tag wird mit der zuletzt besuchte Seite ersetzt. Kann auch mit
      "link_open", "link_url" und "link_title" verwendet werden.</td>
</tr>
<tr>
  <td><code>{{link::login}}</code></td>
  <td>Dieses Tag wird mit einem Link zur Anmeldeseite des aktuellen
      Frontend-Benutzers (falls vorhanden) ersetzt.</td>
</tr>
<tr>
  <td><code>{{link_open::*}}</code></td>
  <td>Wird mit dem öffnenden Tag eines Links zu einer internen Seite ersetzt:
      <code>{{link_open::12}}Hier klicken{{link_close}}</code>.</td>
</tr>
<tr>
  <td><code>{{link_url::*}}</code></td>
  <td>Dieses Tag wird mit der URL einer internen Seite ersetzt: <code>&lt;a
      href="{{link_url::12}}"&gt;Hier klicken&lt;/a&gt;</code>.</td>
</tr>
<tr>
  <td><code>{{link_title::*}}</code></td>
  <td>Dieses Tag wird mit dem Titel einer internen Seite ersetzt: <code>&lt;a
      title="{{link_title::12}}"&gt;Hier klicken&lt;/a&gt;</code>.</td>
</tr>
<tr>
  <td><code>{{link_close}}</code></td>
  <td>Wird mit dem schließenden Tag eines Links zu einer internen Seite
      ersetzt: <code>{{link_open::12}}Hier klicken{{link_close}}</code>.</td>
</tr>
<tr>
  <td><code>{{article::*}}</code></td>
  <td>Dieses Tag wird mit einem Link zu einem Artikel ersetzt (ersetzen Sie *
      mit der ID oder dem Alias).</td>
</tr>
<tr>
  <td><code>{{article_open::*}}</code></td>
  <td>Wird mit dem öffnenden Tag eines Links zu einem Artikel ersetzt:
      <code>{{article_open::12}}Hier klicken{{link_close}}</code>.</td>
</tr>
<tr>
  <td><code>{{article_url::*}}</code></td>
  <td>Dieses Tag wird mit der URL eines Artikels ersetzt: <code>&lt;a
      href="{{article_url::12}}"&gt;Hier klicken&lt;/a&gt;</code>.</td>
</tr>
<tr>
  <td><code>{{article_title::*}}</code></td>
  <td>Dieses Tag wird mit dem Titel eines Artikels ersetzt: <code>&lt;a
      title="{{article_title::12}}"&gt;Hier klicken&lt;/a&gt;</code>.</td>
</tr>
<tr>
  <td><code>{{news::*}}</code></td>
  <td>Dieses Tag wird mit einem Link zu einer Nachricht ersetzt (ersetzen Sie *
      mit der ID oder dem Alias).</td>
</tr>
<tr>
  <td><code>{{news_open::*}}</code></td>
  <td>Wird mit dem öffnenden Tag eines Links zu einer Nachricht ersetzt:
      <code>{{news_open::12}}Hier klicken{{link_close}}</code>.</td>
</tr>
<tr>
  <td><code>{{news_url::*}}</code></td>
  <td>Dieses Tag wird mit der URL einer Nachricht ersetzt: <code>&lt;a
      href="{{news_url::12}}"&gt;Hier klicken&lt;/a&gt;</code>.</td>
</tr>
<tr>
  <td><code>{{news_title::*}}</code></td>
  <td>Dieses Tag wird mit dem Titel einer Nachricht ersetzt: <code>&lt;a
      title="{{news_title::12}}"&gt;Hier klicken&lt;/a&gt;</code>.</td>
</tr>
<tr>
  <td><code>{{event::*}}</code></td>
  <td>Dieses Tag wird mit einem Link zu einem Event ersetzt (ersetzen Sie * mit
      der ID oder dem Alias).</td>
</tr>
<tr>
  <td><code>{{event_open::*}}</code></td>
  <td>Wird mit dem öffnenden Tag eines Links zu einem Event ersetzt:
      <code>{{event_open::12}}Hier klicken{{link_close}}</code>.</td>
</tr>
<tr>
  <td><code>{{event_url::*}}</code></td>
  <td>Dieses Tag wird mit der URL eines Events ersetzt: <code>&lt;a
      href="{{event_url::12}}"&gt;Hier klicken&lt;/a&gt;</code>.</td>
</tr>
<tr>
  <td><code>{{event_title::*}}</code></td>
  <td>Dieses Tag wird mit dem Titel eines Events ersetzt: <code>&lt;a
      title="{{event_title::12}}"&gt;Hier klicken&lt;/a&gt;</code>.</td>
</tr>
<tr>
  <td><code>{{faq::*}}</code></td>
  <td>Dieses Tag wird mit einem Link zu einer häufig gestellten Frage ersetzt
      (ersetzen Sie * mit der ID oder dem Alias).</td>
</tr>
<tr>
  <td><code>{{faq_open::*}}</code></td>
  <td>Wird mit dem öffnenden Tag eines Links zu einer Frage ersetzt:
      <code>{{faq_open::12}}Hier klicken{{link_close}}</code>.</td>
</tr>
<tr>
  <td><code>{{faq_url::*}}</code></td>
  <td>Dieses Tag wird mit der URL einer Frage ersetzt: <code>&lt;a
      href="{{faq_url::12}}"&gt;Hier klicken&lt;/a&gt;</code>.</td>
</tr>
<tr>
  <td><code>{{faq_title::*}}</code></td>
  <td>Dieses Tag wird mit dem Titel einer Frage ersetzt: <code>&lt;a
      title="{{faq_title::12}}"&gt;Hier klicken&lt;/a&gt;</code>.</td>
</tr>
</table>


### Benutzereigenschaften

Mit den folgenden Inserttags können Eigenschaften des angemeldeten Benutzers
ausgebeben werden.

<table>
<tr>
  <th>Insert-Tag</th>
  <th>Beschreibung</th>
</tr>
<tr>
  <td><code>{{user::firstname}}</code></td>
  <td>Dieses Tag wird mit dem Vornamen des angemeldeten Benutzers ersetzt.</td>
</tr>
<tr>
  <td><code>{{user::lastname}}</code></td>
  <td>Dieses Tag wird mit dem Nachnamen des angemeldeten Benutzers ersetzt.</td>
</tr>
<tr>
  <td><code>{{user::company}}</code></td>
  <td>Dieses Tag wird mit dem Firmennamen des angemeldeten Benutzers
      ersetzt.</td>
</tr>
<tr>
  <td><code>{{user::phone}}</code></td>
  <td>Dieses Tag wird mit der Telefonnummer des angemeldeten Benutzers
      ersetzt.</td>
</tr>
<tr>
  <td><code>{{user::mobile}}</code></td>
  <td>Dieses Tag wird mit der Handynummer des angemeldeten Benutzers
      ersetzt.</td>
</tr>
<tr>
  <td><code>{{user::fax}}</code></td>
  <td>Dieses Tag wird mit der Faxnummer des angemeldeten Benutzers ersetzt.</td>
</tr>
<tr>
  <td><code>{{user::email}}</code></td>
  <td>Dieses Tag wird mit der E-Mail-Adresse des angemeldeten Benutzers
      ersetzt.</td>
</tr>
<tr>
  <td><code>{{user::website}}</code></td>
  <td>Dieses Tag wird mit der Internetadresse des angemeldeten Benutzers
      ersetzt.</td>
</tr>
<tr>
  <td><code>{{user::street}}</code></td>
  <td>Dieses Tag wird mit dem Staßennamen des angemeldeten Benutzers
      ersetzt.</td>
</tr>
<tr>
  <td><code>{{user::postal}}</code></td>
  <td>Dieses Tag wird mit der Postleitzahl des angemeldeten Benutzers
      ersetzt.</td>
</tr>
<tr>
  <td><code>{{user::city}}</code></td>
  <td>Dieses Tag wird mit der Stadt des angemeldeten Benutzers ersetzt.</td>
</tr>
<tr>
  <td><code>{{user::country}}</code></td>
  <td>Dieses Tag wird mit dem Land des angemeldeten Benutzers ersetzt.</td>
</tr>
<tr>
  <td><code>{{user::username}}</code></td>
  <td>Dieses Tag wird mit dem Benutzernamen des angemeldeten Benutzers
      ersetzt.</td>
</tr>
</table>


### Seiteneigenschaften

Mit den folgenden Inserttags können Seiteneigenschaften wie z.B. der Seitenname
ausgegeben werden.

<table>
<tr>
  <th>Insert-Tag</th>
  <th>Beschreibung</th>
</tr>
<tr>
  <td><code>{{page::id}}</code></td>
  <td>Dieses Tag wird mit der ID der aktuellen Seite ersetzt.</td>
</tr>
<tr>
  <td><code>{{page::alias}}</code></td>
  <td>Dieses Tag wird mit dem Alias der aktuellen Seite ersetzt.</td>
</tr>
<tr>
  <td><code>{{page::title}}</code></td>
  <td>Dieses Tag wird mit dem Namen der aktuellen Seite ersetzt.</td>
</tr>
<tr>
  <td><code>{{page::pageTitle}}</code></td>
  <td>Dieses Tag wird mit dem Titel der aktuellen Seite ersetzt.</td>
</tr>
<tr>
  <td><code>{{page::language}}</code></td>
  <td>Dieses Tag wird mit der Sprache der aktuellen Seite ersetzt.</td>
</tr>
<tr>
  <td><code>{{page::parentAlias}}</code></td>
  <td>Dieses Tag wird mit dem Alias der übergeordneten Seite ersetzt.</td>
</tr>
<tr>
  <td><code>{{page::parentTitle}}</code></td>
  <td>Dieses Tag wird mit dem Namen der übergeordneten Seite ersetzt.</td>
</tr>
<tr>
  <td><code>{{page::parentPageTitle}}</code></td>
  <td>Dieses Tag wird mit dem Titel der übergeordneten Seite ersetzt.</td>
</tr>
<tr>
  <td><code>{{page::mainAlias}}</code></td>
  <td>Dieses Tag wird mit dem Alias der übergeordneten Hauptseite ersetzt.</td>
</tr>
<tr>
  <td><code>{{page::mainTitle}}</code></td>
  <td>Dieses Tag wird mit dem Namen der übergeordneten Hauptseite ersetzt.</td>
</tr>
<tr>
  <td><code>{{page::mainPageTitle}}</code></td>
  <td>Dieses Tag wird mit dem Titel der übergeordneten Hauptseite ersetzt.</td>
</tr>
<tr>
  <td><code>{{page::rootTitle}}</code></td>
  <td>Dieses Tag wird mit dem Namen der Webseite ersetzt.</td>
</tr>
<tr>
  <td><code>{{page::rootPageTitle}}</code></td>
  <td>Dieses Tag wird mit dem Titel der Webseite ersetzt.</td>
</tr>
</table>


### Umgebungsvariablen

Mit den folgenden Inserttags können Umgebungsvariablen wie z.B. der Seitenname
oder der Request-String ausgegeben werden.

<table>
<tr>
  <th>Insert-Tag</th>
  <th>Beschreibung</th>
</tr>
<tr>
  <td><code>{{env::host}}</code></td>
  <td>Dieses Tag wird mit dem aktuellen Hostnamen ersetzt.</td>
</tr>
<tr>
  <td><code>{{env::url}}</code></td>
  <td>Dieses Tag wird mit dem Hostnamen und dem Protokoll ersetzt.</td>
</tr>
<tr>
  <td><code>{{env::path}}</code></td>
  <td>Dieses Tag wird mit der aktuellen Basis-URL samt Pfad zum
      Contao-Verzeichnis ersetzt.</td>
</tr>
<tr>
  <td><code>{{env::request}}</code></td>
  <td>Dieses Tag wird mit dem aktuellen Request-String ersetzt.</td>
</tr>
<tr>
  <td><code>{{env::ip}}</code></td>
  <td>Dieses Tag wird mit der IP-Adresse des aktuellen Besuchers ersetzt.</td>
</tr>
<tr>
  <td><code>{{env::referer}}</code></td>
  <td>Dieses Tag wird mit der URL der zuletzt besuchten Seite ersetzt.</td>
</tr>
<tr>
  <td><code>{{env::files_url}}</code></td>
  <td>Dieses Tag wird mit der statischen URL des Uploadverzeichnis ersetzt.</td>
</tr>
<tr>
  <td><code>{{env::assets_url}}</code></td>
  <td>Dieses Tag wird mit der statischen URL des Assets-Verzeichnis ersetzt.</td>
</tr>
</table>


### Include-Elemente

Mit den folgenden Inserttags können Ressourcen wie z.B. Artikel, Module oder
Dateien aus dem "templates"-Verzeichnis eingebunden werden.

<table>
<tr>
  <th>Insert-Tag</th>
  <th>Beschreibung</th>
</tr>
<tr>
  <td><code>{{insert_article::*}}</code></td>
  <td>Dieses Tag wird mit dem referenzierten Artikel ersetzt (ersetzen Sie * mit
      der ID oder dem Alias).</td>
</tr>
<tr>
  <td><code>{{insert_content::*}}</code></td>
  <td>Dieses Tag wird mit dem referenzierten Inhaltselement ersetzt (ersetzen
      Sie * mit der ID des Elements).</td>
</tr>
<tr>
  <td><code>{{insert_module::*}}</code></td>
  <td>Dieses Tag wird mit dem referenzierten Modul ersetzt (ersetzen Sie * mit
      der ID des Moduls).</td>
</tr>
<tr>
  <td><code>{{insert_form::*}}</code></td>
  <td>Dieses Tag wird mit dem referenzierten Formular ersetzt (ersetzen Sie * mit
      der ID des Formulars).</td>
</tr>
<tr>
  <td><code>{{article_teaser::*}}</code></td>
  <td>Dieses Tag wird mit dem Teaser eines Artikels ersetzt (ersetzen Sie * mit
      der ID des Artikels).</td>
</tr>
<tr>
  <td><code>{{news_teaser::*}}</code></td>
  <td>Dieses Tag wird mit dem Teaser einer Nachricht ersetzt (ersetzen Sie * mit
      der ID der Nachricht).</td>
</tr>
<tr>
  <td><code>{{event_teaser::*}}</code></td>
  <td>Dieses Tag wird mit dem Teaser eines Events ersetzt (ersetzen Sie * mit
      der ID des Events).</td>
</tr>
<tr>
  <td><code>{{file::*}}</code></td>
  <td>Dieses Tag wird mit dem Inhalt einer .php- oder .tpl-Datei aus dem
      "templates"-Verzeichnis ersetzt (ersetzen Sie * mit dem Namen). Bei Bedarf
      können Sie Argumente übergeben: <code>{{file::file.php?arg1=val}}</code></td>
</tr>
</table>


### Verschiedenes

Mit den folgenden Inserttags können Sie verschiedene Aufgaben erledigen und
z.B. das aktuelle Datum oder ein Lightbox-Bild einfügen.

<table>
<tr>
  <th>Insert-Tag</th>
  <th>Beschreibung</th>
</tr>
<tr>
  <td><code>{{date}}</code></td>
  <td>Dieses Tag wird mit dem aktuellen Datum gemäß des globalen Datumsformats
      ersetzt.</td>
</tr>
<tr>
  <td><code>{{date::*}}</code></td>
  <td>Dieses Tag wird mit dem aktuellen Datum gemäß eines individuellen
      Datumsformats ersetzt.</td>
</tr>
<tr>
  <td><code>{{last_update}}</code></td>
  <td>Dieses Tag wird mit dem Datum der letzten Aktualisierung gemäß des
      globalen Datumsformats ersetzt.</td>
</tr>
<tr>
  <td><code>{{last_update::*}}</code></td>
  <td>Dieses Tag wird mit Datum der letzten Aktualisierung gemäß eines
      individuellen Datumsformats ersetzt.</td>
</tr>
<tr>
  <td><code>{{email::*}}</code></td>
  <td>Dieses Tag wird mit einem verschlüsselten Link zu einer E-Mail-Adresse
      ersetzt.</td>
</tr>
<tr>
  <td><code>{{email_open::*}}</code></td>
  <td>Dieses Tag wird mit einem verschlüsselten Link zu einer E-Mail-Adresse
      ersetzt. Allerdings wird das schließende <code>&lt;/a&gt;</code> nicht
      angefügt.</td>
</tr>
<tr>
  <td><code>{{email_url::*}}</code></td>
  <td>Dieses Tag wird nur durch die verschlüsselte E-Mail-Adresse ersetzt.</td>
</tr>
<tr>
  <td><code>{{lang::*}}</code></td>
  <td>Mit diesem Tag können fremdsprachige Wörter in einem Text markiert
      werden: <code>{{lang::fr}}Au revoir{{lang}}</code>. Dies wird ersetzt mit
      <code>&lt;span lang="fr" xml:lang="fr"&gt;Au revoir&lt;/span&gt;</code>.</td>
</tr>
<tr>
  <td><code>{{abbr::*}}</code></td>
  <td>Abkürzungen in einem Text markieren: <code>{{abbr::World Wide
      Web}}WWW{{abbr}}</code>. Dies wird ersetzt mit <code>&lt;abbr title="World
      Wide Web"&gt;WWW&lt;/abbr&gt;</code>.</td>
</tr>
<tr>
  <td><code>{{acronym::*}}</code></td>
  <td>Akronyme in einem Text markieren: <code>{{acronym::Multipurpose Internet
      Mail Extensions}}MIME{{acronym}}</code>. Dies wird ersetzt mit <code><acronym
      title="Multipurpose Internet Mail Extensions">MIME</acronym></code>.</td>
</tr>
<tr>
  <td><code>{{ua::*}}</code></td>
  <td>Eigenschaften des Browsers (User Agent) ausgeben: <code>{{ua::browser}}</code>.
      Dies wird beispielsweise ersetzt mit "chrome".</td>
</tr>
<tr>
  <td><code>{{iflng::*}}</code></td>
  <td>Dieses Tag wird komplett entfernt, wenn die Sprache der Seite nicht mit
      der Tag-Sprache übereinstimmt. Sie können so sprachspezifische Bezeichnungen
      erstellen: <code>{{iflng::en}}Your name{{iflng}}{{iflng::de}}Ihr Name{{iflng}}</code></td>
</tr>
<tr>
  <td><code>{{ifnlng::*}}</code></td>
  <td>Dieses Tag wird komplett entfernt, wenn die Sprache der Seite mit der
      Tag-Sprache übereinstimmt. Sie können so sprachspezifische Bezeichnungen
      erstellen: <code>{{ifnlng::de}}Your name{{ifnlng}}{{iflng::de}}Ihr Name{{iflng}}</code></td>
</tr>
<tr>
  <td><code>{{image::*}}</code></td>
  <td>Dieses Tag wird mit der Vorschauansicht eines Bildes ersetzt:
      <code>{{image::files/image.jpg?width=200&amp;height=150}}</code>.<br>
      <strong>width</strong>: Breite des Vorschaubildes,<br>
      <strong>height</strong>: Höhe des Vorschaubildes,<br>
      <strong>alt</strong>: Alternativer Text,<br>
      <strong>class</strong>: CSS-Klasse,<br>
      <strong>rel</strong>: rel-Attribut (z.B. "lightbox"),<br>
      <strong>mode</strong>: Modus ("proportional", "crop" oder "box").</td>
</tr>
<tr>
  <td><code>{{label::*}}</code></td>
  <td>Dieses Tag wird mit einer Übersetzung ersetzt: <code>{{label::CNT:au}}</code>
      oder <code>{{label::tl_article:title:0}}</code>. Beachten Sie, dass
      innerhalb des Pfads zur Bezeichnung nur einfache Doppelpunkte verwendet
      werden.</td>
</tr>
<tr>
  <td><code>{{version}}</code></td>
  <td>Dieses Tag wird mit der verwendeten Contao-Version (z.B. 2.11.2)
      ersetzt.</td>
</tr>
<tr>
  <td><code>{{request_token}}</code></td>
  <td>Dieses Tag wird mit dem zur aktuellen Session gehörenden Request-Token
      ersetzt.</td>
</tr>
<tr>
  <td><code>{{toggle_view}}</code></td>
  <td>Dieses Tag wird mit einem Link ersetzt, welcher zwischen Mobile- und
      Desktop-Layout wechselt.</td>
</tr>
</table>

### Inserttag-Flags

Mittels Flags können Sie Insert-Tags weiter verarbeiten. Der Wert kann damit
z.B. einer PHP-Funktion übergeben werden. Beliebig viele Flags können
miteinander kombiniert werden:

```
{{ua::browser|uncached}}
{{page::title|decodeEntities|strtoupper}}
```

Verfügbare Flags:

<table>
<tr>
    <th>Flag</th>
    <th>Beschreibung</th>
    <th>Weitere Informationen</th>
</tr>
<tr>
    <td><code>uncached</code></td>
    <td>Erhält das Tag beim Schreiben der Cache-Datei.</td>
    <td></td>
</tr>
<tr>
    <td><code>refresh</code></td>
    <td>Erstellt die Ausgabe bei jeder Anfrage neu.</td>
    <td></td>
</tr>
<tr>
    <td><code>addslashes</code></td>
    <td>Stellt bestimmten Zeichen eines Strings ein "\" voran.</td>
    <td><a target="_blank" href="http://php.net/addslashes">PHP-Funktion</a></td>
</tr>
<tr>
    <td><code>stripslashes</code></td>
    <td>Entfernt das "\" vor bestimmten Zeichen eines Strings.</td>
    <td><a target="_blank" href="http://php.net/stripslashes">PHP-Funktion</a></td>
</tr>
<tr>
    <td><code>standardize</code></td>
    <td>Standardisiert die Ausgabe (z.B. das Alias bei der Seitenstruktur).</td>
    <td></td>
</tr>
<tr>
    <td><code>ampersand</code></td>
    <td>Wandelt Und-Zeichen in Entities um.</td>
    <td></td>
</tr>
<tr>
    <td><code>specialchars</code></td>
    <td>Wandelt Sonderzeichen in Entities um.</td>
    <td></td>
</tr>
<tr>
    <td><code>nl2br</code></td>
    <td>Fügt vor allen Zeilenumbrüchen eines Strings HTML-Zeilenumbrüche ein.</td>
    <td><a target="_blank" href="http://php.net/nl2br">PHP-Funktion</a></td>
</tr>
<tr>
    <td><code>nl2br_pre</code></td>
    <td>Erhält die Zeilenumbrüche innerhalb von <code>&lt;pre&gt;</code>-Tags.</td>
    <td></td>
</tr>
<tr>
    <td><code>strtolower</code></td>
    <td>Wandelt die Ausgabe in Kleinbuchstaben um.</td>
    <td><a target="_blank" href="http://php.net/strtolower">PHP-Funktion</a></td>
</tr>
<tr>
    <td><code>utf8_strtolower</code></td>
    <td>Unicode-bewusste Umwandlung in Kleinbuchstaben</td>
    <td></td>
</tr>
<tr>
    <td><code>strtoupper</code></td>
    <td>Wandelt die Ausgabe in Großbuchstaben um.</td>
    <td><a target="_blank" href="http://php.net/strtoupper">PHP-Funktion</a></td>
</tr>
<tr>
    <td><code>utf8_strtoupper</code></td>
    <td>Unicode-bewusste Umwandlung in Großbuchstaben</td>
    <td></td>
</tr>
<tr>
    <td><code>ucfirst</code></td>
    <td>Wandelt das erste Zeichen in einen Großbuchstaben um.</td>
    <td><a target="_blank" href="http://php.net/ucfirst">PHP-Funktion</a></td>
</tr>
<tr>
    <td><code>lcfirst</code></td>
    <td>Wandelt das erste Zeichen in einen Kleinbuchstaben um.</td>
    <td><a target="_blank" href="http://php.net/lcfirst">PHP-Funktion</a></td>
</tr>
<tr>
    <td><code>ucwords</code></td>
    <td>Wandelt das erste Zeichen jedes Wortes in einen Großbuchstaben um.</td>
    <td><a target="_blank" href="http://php.net/ucwords">PHP-Funktion</a></td>
</tr>
<tr>
    <td><code>trim</code></td>
    <td>Entfernt Leerzeichen vom Anfang und Ende der Ausgabe.</td>
    <td><a target="_blank" href="http://php.net/trim">PHP-Funktion</a></td>
</tr>
<tr>
    <td><code>rtrim</code></td>
    <td>Entfernt Leerzeichen vom Anfang der Ausgabe.</td>
    <td><a target="_blank" href="http://php.net/rtrim">PHP-Funktion</a></td>
</tr>
<tr>
    <td><code>ltrim</code></td>
    <td>Entfernt Leerzeichen vom Ende der Ausgabe.</td>
    <td><a target="_blank" href="http://php.net/ltrim">PHP-Funktion</a></td>
</tr>
<tr>
    <td><code>utf8_romanize</code></td>
    <td>Romanisiert die Ausgabe.</td>
    <td></td>
</tr>
<tr>
    <td><code>strrev</code></td>
    <td>Dreht die Ausgabe um.</td>
    <td><a target="_blank" href="http://php.net/strrev">PHP-Funktion</a></td>
</tr>
<tr>
    <td><code>encodeEmail</code></td>
    <td>Kodiert E-Mail-Adressen in der Ausgabe.</td>
    <td>siehe <code>String::encodeEmail</code></td>
</tr>
<tr>
    <td><code>decodeEntities</code></td>
    <td>Dekodiert Entities in der Ausgabe.</td>
    <td>siehe <code>String::decodeEntities()</code></td>
</tr>
<tr>
    <td><code>number_format</code></td>
    <td>Formatiert eine Zahl (keine Dezimalstellen).</td>
    <td>siehe <code>System::getFormattedNumber()</code></td>
</tr>
<tr>
    <td><code>currency_format</code></td>
    <td>Formatiert eine Währung (zwei Dezimalstellen).</td>
    <td>siehe <code>System::getFormattedNumber()</code></td>
</tr>
<tr>
    <td><code>readable_size</code></td>
    <td>Wandelt die Ausgabe in ein menschenlesbares Format um.</td>
    <td>siehe <code>System::getReadableSize()</code></td>
</tr>
<tr>
    <td><code>base64_encode</code></td>
    <td>Enkodiert einen Text mittels des 
    <a href="https://de.wikipedia.org/wiki/Base64" 
    target="_blank">Base64-Verfahrens</a>.</td>
    <td><a target="_blank" href="http://php.net/base64_encode">PHP-Funktion</a>
    </td>
</tr>
<tr>
    <td><code>base64_decode</code></td>
    <td>Dekodiert einen Text mittels des 
    <a href="https://de.wikipedia.org/wiki/Base64" 
    target="_blank">Base64-Verfahrens</a>.</td>
    <td><a target="_blank" href="http://php.net/base64_decode">PHP-Funktion</a>
    </td>
</tr>
</table>


[1]: https://contao.org/de/extension-list.html
[2]: http://de.wikipedia.org/wiki/Opt-in
[3]: 04-Managing-content.md#inserttags
[7]: http://de.wikipedia.org/wiki/BBCode
[8]: 03-Managing-pages.md#theme-bestandteile
