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
