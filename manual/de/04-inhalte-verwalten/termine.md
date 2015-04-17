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
