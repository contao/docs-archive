# Inhalte verwalten

Die folgenden Kapitel erklären, wie man Inhalte in Contao verwaltet. Der
Contao-Core beinhaltet bereits die grundlegenden Inhaltstypen wie z.B. Artikel,
Nachrichten, Events, Newsletter oder Formatdefinitionen. Weitere Inhaltstypen
wie Banner, Tickets, Produkte oder Empfehlungen sind über das [Extension
Repository][1] verfügbar. Inhalte können im Backend mit den entsprechenden
Modulen angelegt werden.


## Artikel

Artikel sind Container für Inhaltselemente. Das Gruppieren zusammengehöriger
Inhaltselement macht es einfach, sie alle auf einmal zu verschieben, zu
veröffentlichen, zu kopieren oder zu exportieren, anstatt jedes einzelne
Element zu bearbeiten. Jeder Artikel ist mit einer bestimmten Seite und einem
Layoutbereich assoziiert und hat daher eine feste Position innerhalb der
Seitenstruktur und auf der Webseite.


### Inhaltselemente

Inhaltselemente sind ein einfacher und intuitiver Weg, um Inhalte zuerstellen.
Anstatt nur den Rich Text Editor zu verwenden, bietet Contao für jeden
Inhaltstyp wie z.B. Texte, Listen, Tabellen,Hyperlinks, Bilder oder Downloads
ein eigenes Element. Nachfolgendfinden Sie eine Übersicht über die im
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
  <td>Erzeugt einen Rich Text, der mit [TinyMCE][2] formatiert werden kann.</td>
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
  <td>Akkordeon</td>
  <td>ce_accordion</td>
  <td>Erzeugt ein [MooTools][3] Akkordeon-Element.</td>
</tr>
<tr>
  <td>Code</td>
  <td>ce_code</td>
  <td>Gibt formatierten Programmcode auf dem Bildschirm aus.</td>
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
  <td>Erzeugt eine [lightbox][4] Bildergalerie.</td>
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

![](https://raw.github.com/contao/docs/2.11/book/de/images/geschuetztes-element.jpg)


### Flash-Inhalte

Flash-Inhalte sind spezielle Inhalte, die nicht als Artikel auf der Webseite
ausgegeben, sondern mittels `loadVars()` in einen dynamischen Flash-Film geladen
werden. Fügen Sie folgendesSkript in Ihren Flash-Film ein, um die Kommunikation
mit Contao zuermöglichen:

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
Thema beziehen und die Beiträge können als RSS- oder Atom-Feed exportiert
werden.

![](https://raw.github.com/contao/docs/2.11/book/de/images/newsfeed.jpg)


### Frontend-Module

Mit den Frontend-Modulen der News/Blog-Erweiterung können Nachrichtenauf der
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
  <td>mod_newsarchiveMenu</td>
  <td>Erzeugt ein Menü zur Navigation des Nachrichtenarchivs.</td>
</tr>
</table>


### Permalinks

Jede Nachricht hat eine eindeutige URL (Permalink), die zur Referenzierung des
Beitrags verwendet werden kann:

```
http://www.domain.com/news/items/james-wilson-returns.html
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

Kalender werden zur Gruppierung und/oder Kategorisierung von Terminenverwendet.
Jeder Kalender kann sich auf eine bestimmte Sprache oder einbestimmtes Thema
beziehen und die Termine können als RSS- oderAtom-Feed exportiert werden.

![](https://raw.github.com/contao/docs/2.11/book/de/images/kalender-feed.jpg)


### Frontend-Module

Mit den Frontend-Modulen der Kalender-Erweiterung können Termine bzw. Eventsauf
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
  <td>mod_event</td>
  <td>Stellt einen einzelnen Event dar.</td>
</tr>
<tr>
  <td>Eventliste</td>
  <td>mod_eventlist</td>
  <td>Listet alle Events eines bestimmten Zeitraums auf.</td>
</tr>
<tr>
  <td>Nächste Events</td>
  <td>mod_eventlist</td>
  <td>Listet alle demnächst stattfindenden Events auf.</td>
</tr>
</table>


### Permalinks

Jeder Termin hat eine eindeutige URL (Permalink), die zur Referenzierung des
Events verwendet werden kann:

```
http://www.domain.com/event-reader/events/final-exams.html
```

Die oben genannte URL fordert den Event "final-exams" auf der Seite "events" an.
Denken sie daran, dass Contao ein Seiten-basiertes CMS ist; gäbe es die Seite
"events" nicht oder enthielte sie nicht das Modul Eventleser, würde der Beitrag
auch nicht angezeigt.


## Newsletter

Die Newsletter-Erweiterung ermöglicht das Versenden von Newslettern, die
Verwaltung von Abonnements sowie die optionale Ausgabe versendeter Nachrichten
im Frontend. Im Gegensatz zu Artikeln, die mit einer bestimmten Seite assoziiert
sind, werden Newsletter in Verteilern organisiert und können so einfach
gruppiert oder kategorisiert werden.


### Abonnenten

Newsletter-Abonnements werden normalerweise automatisch über die entsprechenden
Frontend-Module verwaltet, ohne dass Sie in den Prozess eingreifen müssten. Aus
Datenschutzrechtlichen Gründen muss das Abonnieren eines Verteilers mittels
[Double Opt-In][5] erfolgen und es wird nur die E-Mail-Adresse des Abonnements
gespeichert.

![](https://raw.github.com/contao/docs/2.11/book/de/images/newsletter-abonnenten.jpg)

Falls Sie bereits einen Verteiler haben, können Sie die Abonnenten aus einer
CSV-Datei in Contao importieren.


### Newsletter personalisieren

Insofern Sie Newsletter an registrierte Mitglieder verschicken, können Sie
diese mit Hilfe der sogenannten "Simple Tokens" personalisieren. Simple Tokens
funktionieren ähnlich wie [Inserttags][6] und können sowohl im HTML- als auch
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

![](https://raw.github.com/contao/docs/2.11/book/de/images/newsletter-versenden.jpg)


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
  <td>nl_default</td>
  <td>Erzeugt ein Formular zum Abonnieren von Verteilern.</td>
</tr>
<tr>
  <td>Kündigen</td>
  <td>nl_default</td>
  <td>Erzeugt ein Formular zum Kündigen von Abonnements.</td>
</tr>
<tr>
  <td>Newsletterliste</td>
  <td>mod_newsletter_list</td>
  <td>Fügt der Seite eine Newsletterliste hinzu.</td>
</tr>
<tr>
  <td>Newsletterleser</td>
  <td>mod_newsletter_reader</td>
  <td>Stellt einen einzelnen Newsletter dar.</td>
</tr>
</table>


### Permalinks

Jeder Newsletter hat eine eindeutige URL (Permalink), die zur Referenzierung der
Nachricht verwendet werden kann:

```
http://www.domain.com/newsletters/items/james-wilson-returns.html
```

Die obige URL fordert den Newsletter "james-wilson-returns" auf der Seite
"newsletters" an. Denken sie daran, dass Contao ein Seiten-basiertes CMS ist;
gäbe es die Seite "newsletters" nicht oder enthielte sie nicht das Modul
Newsletterleser, würde der Beitrag auch nicht angezeigt.


## Formulare

Mit dem Formulargenerator lassen sich interaktive Formulare erstellen,die per
E-Mail verschickt oder in der Datenbank gespeichert werdenkönnen. Hochgeladene
Dateien werden als Anhang versendet oder aufdem Server gespeichert. Folgende
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
  <td>Textfeld</td>
  <td>text</td>
  <td>Ein einzeiliges Eingabefeld für einen kurzen oder mittellangen Text.</td>
</tr>
<tr>
  <td>Passwortfeld</td>
  <td>password</td>
  <td>Ein einzeiliges Eingabefeld für ein Passwort.</td>
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
  <td>Eine einfache Rechenaufgabe zum Schutz gegen Spam-Bots (CAPTCHA).</td>
</tr>
<tr>
  <td>Absendefeld</td>
  <td>submit</td>
  <td>Eine Absende-Schaltfläche zur Versendung des Formulars.</td>
</tr>
</table>


## Inserttags

Inserttags sind Platzhalter, die bei der Ausgabe einer Seite durch bestimmte
Inhalte ersetzt werden. So kann beispielsweise das aktuelle Datum angezeigt oder
ein Benutzer mit seinem Namen angesprochen werden. Inserttags können fast
überall in Contao verwendet werden.


### Link-Elemente

Mit den folgenden Inserttags können Seiten und Artikel anhand ihrer ID oder
ihres Alias verlinkt werden.

<table>
<tr>
  <th>Insert-Tag</th>
  <th>Beschreibung</th>
</tr>
<tr>
  <td><code>{{link::*}}</code></td>
  <td>Dieses Tag wird mit einem Link zu einer interne Seite ersetzt (ersetzen
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
      `{{link_open::12}}Click here{{link_close}}`.</td>
</tr>
<tr>
  <td><code>{{link_url::*}}</code></td>
  <td>Dieses Tag wird mit der URL einer internen Seite ersetzt: `<a
      href="{{link_url::12}}">Click here</a>`.</td>
</tr>
<tr>
  <td><code>{{link_title::*}}</code></td>
  <td>Dieses Tag wird mit dem Titel einer internen Seite ersetzt: `<a
      title="{{link_title::12}}">Click here</a>`.</td>
</tr>
<tr>
  <td><code>{{link_close}}</code></td>
  <td>Wird mit dem schließenden Tag eines Links zu einer internen Seite
      ersetzt: `{{link_open::12}}Click here{{link_close}}`.</td>
</tr>
<tr>
  <td><code>{{article::*}}</code></td>
  <td>Dieses Tag wird mit einem Link zu einem Artikel ersetzt (ersetzen Sie *
      mit der ID oder dem Alias).</td>
</tr>
<tr>
  <td><code>{{article_open::*}}</code></td>
  <td>Wird mit dem öffnenden Tag eines Links zu einem Artikel ersetzt:
      `{{article_open::12}}Click here{{link_close}}`.</td>
</tr>
<tr>
  <td><code>{{article_url::*}}</code></td>
  <td>Dieses Tag wird mit der URL eines Artikels ersetzt: `<a
      href="{{article_url::12}}">Click here</a>`.</td>
</tr>
<tr>
  <td><code>{{article_title::*}}</code></td>
  <td>Dieses Tag wird mit dem Titel eines Artikels ersetzt: `<a
      title="{{article_title::12}}">Click here</a>`.</td>
</tr>
<tr>
  <td><code>{{news::*}}</code></td>
  <td>Dieses Tag wird mit einem Link zu einer Nachricht ersetzt (ersetzen Sie *
      mit der ID oder dem Alias).</td>
</tr>
<tr>
  <td><code>{{news_open::*}}</code></td>
  <td>Wird mit dem öffnenden Tag eines Links zu einer Nachricht ersetzt:
      `{{news_open::12}}Click here{{link_close}}`.</td>
</tr>
<tr>
  <td><code>{{news_url::*}}</code></td>
  <td>Dieses Tag wird mit der URL einer Nachricht ersetzt: `<a
      href="{{news_url::12}}">Click here</a>`.</td>
</tr>
<tr>
  <td><code>{{news_title::*}}</code></td>
  <td>Dieses Tag wird mit dem Titel einer Nachricht ersetzt: `<a
      title="{{news_title::12}}">Click here</a>`.</td>
</tr>
<tr>
  <td><code>{{event::*}}</code></td>
  <td>Dieses Tag wird mit einem Link zu einem Event ersetzt (ersetzen Sie * mit
      der ID oder dem Alias).</td>
</tr>
<tr>
  <td><code>{{event_open::*}}</code></td>
  <td>Wird mit dem öffnenden Tag eines Links zu einem Event ersetzt:
      `{{event_open::12}}Click here{{link_close}}`.</td>
</tr>
<tr>
  <td><code>{{event_url::*}}</code></td>
  <td>Dieses Tag wird mit der URL eines Events ersetzt: `<a
      href="{{event_url::12}}">Click here</a>`.</td>
</tr>
<tr>
  <td><code>{{event_title::*}}</code></td>
  <td>Dieses Tag wird mit dem Titel eines Events ersetzt: `<a
      title="{{event_title::12}}">Click here</a>`.</td>
</tr>
<tr>
  <td><code>{{faq::*}}</code></td>
  <td>Dieses Tag wird mit einem Link zu einer häufig gestellten Frage ersetzt
      (ersetzen Sie * mit der ID oder dem Alias).</td>
</tr>
<tr>
  <td><code>{{faq_open::*}}</code></td>
  <td>Wird mit dem öffnenden Tag eines Links zu einer Frage ersetzt:
      `{{faq_open::12}}Click here{{link_close}}`.</td>
</tr>
<tr>
  <td><code>{{faq_url::*}}</code></td>
  <td>Dieses Tag wird mit der URL einer Frage ersetzt: `<a
      href="{{faq_url::12}}">Click here</a>`.</td>
</tr>
<tr>
  <td><code>{{faq_title::*}}</code></td>
  <td>Dieses Tag wird mit dem Titel einer Frage ersetzt: `<a
      title="{{faq_title::12}}">Click here</a>`.</td>
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
  <td><code>{{env::script_url}}</code></td>
  <td>Dieses Tag wird mit der statischen URL des Skriptverzeichnis ersetzt.</td>
</tr>
<tr>
  <td><code>{{env::plugins_url}}</code></td>
  <td>Dieses Tag wird mit der statischen URL des Pluginsverzeichnis
      ersetzt.</td>
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
      `templates`-Verzeichnis ersetzt (ersetzen Sie * mit dem Namen). Bei Bedarf
      können Sie Argumente übergeben: `{{file::file.php?arg1=val}}</code></td>
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
  <td><code>{{lang::*}}</code></td>
  <td>Mit diesem Tag können fremdsprachige Wörter in einem Text markiert
      werden: `{{lang::fr}}Au revoir{{lang}}`. Dies wird ersetzt mit `<span
      lang="fr" xml:lang="fr">Au revoir</span>`.</td>
</tr>
<tr>
  <td><code>{{abbr::*}}</code></td>
  <td>Abkürzungen in einem Text markieren: `{{abbr::World Wide
      Web}}WWW{{abbr}}`. Dies wird ersetzt mit `<abbr title="World Wide
      Web">WWW</abbr>`.</td>
</tr>
<tr>
  <td><code>{{acronym::*}}</code></td>
  <td>Acronyme in einem Text markieren: `{{acronym:: Multipurpose Internet Mail
      Extensions}}MIME{{acronym}}`. Dies wird ersetzt mit `<acronym
      title="Multipurpose Internet Mail Extensions">MIME</acronym>`.</td>
</tr>
<tr>
  <td><code>{{ua::*}}</code></td>
  <td>Eigenschaften des Browsers (User Agent) ausgeben: `{{ua::browser}}`. Dies
      wird beispielsweise ersetzt mit "chrome".</td>
</tr>
<tr>
  <td><code>{{iflng::*}}</code></td>
  <td>Dieses Tag wird komplett entfernt, wenn die Sprache der Seite nicht mit
      der Tag-Sprache übereinstimmt. Sie können so sprachspezifische Bezeichnungen
      erstellen: `{{iflng::en}}Your name{{iflng}}</code></td>
</tr>
<tr>
  <td><code>{{ifnlng::*}}</code></td>
  <td>Dieses Tag wird komplett entfernt, wenn die Sprache der Seite mit der
      Tag-Sprache übereinstimmt. Sie können so sprachspezifische Bezeichnungen
      erstellen: `{{ifnlng::de}}Your name{{iflng}}</code></td>
</tr>
<tr>
  <td><code>{{image::*}}</code></td>
  <td>Dieses Tag wird mit der Vorschauansicht eines Bildes ersetzt:
      `{{image::files/image.jpg?width=200&amp;height=150}}`. **width** Breite
      des Vorschaubildes, **height** Höhe des Vorschaubildes, **alt**
      Alternativer Text, **class** CSS-Klasse, **rel** rel-Attribut (z.B.
      "lightbox"), **mode** Modus ("proportional", "crop" oder "box")</td>
</tr>
<tr>
  <td><code>{{label::*}}</code></td>
  <td>Dieses Tag wird mit einer Übersetzung ersetzt: `{{label::CNT:au}}` oder
      `{{label::tl_article:title:0}}`. Beachten Sie, dass innerhalb des Pfads
      zur Bezeichnung nur einfache Doppelpunkte verwendet werden.</td>
</tr>
<tr>
  <td><code>{{version::*}}</code></td>
  <td>Dieses Tag wird mit der verwendeten Contao-Version (z.B. 2.11.2)
      ersetzt.</td>
</tr>
<tr>
  <td><code>{{request_token::*}}</code></td>
  <td>Dieses Tag wird mit dem zur aktuellen Session gehörenden Request-Token
      ersetzt.</td>
</tr>
</table>


[1]: https://contao.org/de/extension-list.html
[2]: http://tinymce.moxiecode.com
[3]: http://mootools.net
[4]: http://www.digitalia.be/software/slimbox
[5]: http://de.wikipedia.org/wiki/Opt-in
[6]: 04-Inhalte-verwalten.md#inserttags
