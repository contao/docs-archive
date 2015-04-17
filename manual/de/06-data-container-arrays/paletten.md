## Paletten

Eine Palette besteht aus mehreren Formularfeldern, die zur Bearbeitung eines
Datensatzes benötigt werden. Dabei sind meistens nicht alle Spalten einer
Tabelle enthalten, sondern nur die, die zu einem bestimmten Modul oder Element
gehören. Paletten können sich je nach Benutzerrechten oder Elementtyp
dynamisch ändern und Teile des Formulars (Subpaletten) können interaktiv per
Ajax nachgeladen werden.


### Gruppen definieren

Eine Palette ist eine Reihung mehrerer Feldnamen, die durch einen Strichpunkt
(;) oder ein Komma (,) verbunden sind. Während das Komma nur zur Abgrenzung der
Feldnamen verwendet wird, markiert der Strichpunkt den Beginn einer neuen
Gruppe, die aus- und eingeklappt werden kann.

![](images/paletten.jpg?raw=true)

Das obige Beispiel wird durch folgenden Code definiert:

```php
{title_legend},headline,alias,author;{date_legend},date,time;{teaser_legend:hide},subheadline,teaser
```

Die Platzhalter `title_legend` und `date_legend` werden durch die entsprechenden
Übersetzungen im "TL_LANG"-Array ersetzt.

```
$GLOBALS['TL_LANG']['tl_news']['title_legend'] = 'Titel und Autor';
$GLOBALS['TL_LANG']['tl_news']['date_legend']  = 'Datum und Uhrzeit';
```


### Felder ausrichten

Das Contao-Backend verwendet ein 2-spaltiges Grid-System, um Formularfelder
innerhalb ihrer Gruppen auszurichten. Folgende CSS-Klassen können in der
"eval"-Sektion des Data Container Arrays als `tl_class` vergeben werden (z.B.
`'tl_class'=>'w50 wizard'`):

<table>
<tr>
  <th>tl_class</th>
  <th>Beschreibung</th>
</tr>
<tr>
  <td>w50</td>
  <td>Setzt die Feldbreite auf 50% und floatet das Element
      (<code>float:left</code>).</td>
</tr>
<tr>
  <td>clr</td>
  <td>Hebt alle Floats auf (<code>clear:both</code>).</td>
</tr>
<tr>
  <td>wizard</td>
  <td>Verkürzt das Eingabefeld, damit genug Platz für den Wizard (z.B. Date
      Picker) ist.</td>
</tr>
<tr>
  <td>long</td>
  <td>Lässt das Eingabefeld zwei Spalten umspannen.</td>
</tr>
<tr>
  <td>m12</td>
  <td>Fügt dem Element einen oberen Abstand von 12 Pixeln hinzu (z.B. für
      einzelne Checkboxen).</td>
</tr>
</table>
