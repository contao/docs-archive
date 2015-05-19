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

Der Besucher kann ausserdem die [BBCode Sprache][1] verwenden.
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


[1]: http://de.wikipedia.org/wiki/BBCode
