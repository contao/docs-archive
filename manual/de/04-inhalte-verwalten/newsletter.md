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
[Double Opt-In][1] erfolgen und es wird nur die E-Mail-Adresse des Abonnements
gespeichert.

![](images/newsletter-abonnenten.jpg?raw=true)

Falls Sie bereits einen Verteiler haben, können Sie die Abonnenten aus einer
CSV-Datei in Contao importieren.


### Newsletter personalisieren

Insofern Sie Newsletter an registrierte Mitglieder verschicken, können Sie
diese mit Hilfe der sogenannten "Simple Tokens" personalisieren. Simple Tokens
funktionieren ähnlich wie [Inserttags][2] und können sowohl im HTML- als auch
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


[1]: http://de.wikipedia.org/wiki/Opt-in
[2]: ../04-inhalte-verwalten/inserttags.md#inserttags