# Administrationsbereich

Um den Administrationsbereich (Backend) aufzurufen, hängen Sie einfach
`/contao` an die URL Ihrer Contao-Webseite an. Die Konten sind gegen Brute
Force-Attacken geschützt und werden für 5 Minuten gesperrt, wenn dreimal
hintereinander ein falsches Passwort eingegeben wurde.


## Datensätze auflisten

Die Contao Core-Engine unterstützt drei Ansichten: eine einfache Liste ("list
view"), eine nach der übergeordneten Tabelle gruppierte Liste ("parent view")
und eine hierarchische Liste ("tree view"). Diese drei Ansichten werden zur
Darstellung der Daten im Backend verwendet.


### List View

Der "List View" listet die Datensätze einer Tabelle in einer bestimmten
Reihenfolge auf, normalerweise gruppiert nach Anfangsbuchstabe.

![](images/list-view-de.jpg?raw=true)


### Parent View

Der "Parent View" listet die Datensätze einer Kindtabelle auf, die sich auf
einen Datensatz der Elterntabelle beziehen. Eltern-Kind-Relationen kommen
häufig vor in Contao, z.B. bei Artikeln und Inhaltselementen, Archiven und
Nachrichten oder Stylesheets und Formatdefinitionen.

![](images/parent-view-de.jpg?raw=true)


### Tree View

Der "Tree View" listet Datensätze auf, die in einer hierarchischen Struktur
organisiert sind. Contao unterstützt sowohl hierarchische Beziehungen innerhalb
einer Tabelle (z.B. Seitenstruktur) als auch Kindtabellen, die sich auf
hierarchische Elterntabellen beziehen (z.B. Artikel und Seiten).

![](images/tree-view-de.jpg?raw=true)


### Daten sortieren und filtern

Contao bietet mehrere Möglichkeiten, Auflistungen zu sortieren und zu filtern,
damit Sie auch bei mehreren tausend Datensätzen den Überblick behalten. Viele
Listen können anhand eines oder mehrerer Felder eingeschränkt werden. Die
meisten bieten zusätzlich eine Volltext-Suche an, die sogar reguläre
Ausdrücke unterstützt. Um die Ladezeit zu optimieren, zeigt Contao immer nur
30 Datensätze auf einmal an.

![](images/sortieren-und-filtern.jpg?raw=true)


## Datensätze bearbeiten

Contao bietet etliche professionelle Funktionen, die das Bearbeiten von Daten so
einfach und komfortabel wie möglich machen. Sie können zu früheren Versionen
zurück gehen, gelöschte Datensätze wiederherstellen, Elemente via Clipboard
verschieben und sogar mehrere Datensätze auf einmal bearbeiten. Die meisten
dieser Funktionen sind über die Navigationssymbole aufrufbar.


### Icons im List View

Der "List View" als einfachste Ansicht bietet nur die vier grundlegenden
Befehle: bearbeiten, duplizieren, löschen und Info.

![](images/list-view-icons-de.jpg?raw=true)


### Icons im Parent View

Der "Parent View" bietet zwei zusätzliche Icons, um die Reihenfolge der
Datensätze zu kontrollieren. Die Reihenfolge kann auch mittels Drag & Drop
geändert werden. Dazu einfach auf das "Drag & Drop" Icon klicken und
an die neue Position bewegen.

![](images/parent-view-icons-de.jpg?raw=true)


### Icons im Tree View

Im "Tree View" werden weitere Icons benötigt, um die hierarchische Struktur
abbilden zu können. Neben dem Kopieren eines einzelnen Datensatzes können auch
ganze Teilbäume dupliziert und entweder in einen oder nach einem anderen
Datensatz eingefügt werden.

![](images/tree-view-icons-de.jpg?raw=true)


### Frühere Versionen wiederherstellen

Contao erstellt bei jedem Speichervorgang automatisch eine neue Version eines
Datensatzes. Sobald es mehr als eine Version gibt, erscheint oberhalb des
Formulars ein Drop-Down-Menü, mit dem Sie zu einer früheren Versionen zurück
gehen können.

Durch Klick auf das Icon rechts des Drop-Down-Menü werden die Unterschiede
zwischen der aktuelle und der gewählten Version angezeigt.

![](images/versionierung.jpg?raw=true)


### Mehrere Datensätze bearbeiten

Die Möglichkeit, mehrere Datensätze auf einmal zu bearbeiten, hebt Contao klar
von den Mitbewerbern ab. Wechseln Sie den Bearbeitungsmodus durch Anklicken der
"Mehrere bearbeiten"-Schaltfläche und wählen Sie dann die zu bearbeitenden
Datensätze und Felder aus.

![](images/mehrere-datensaetze-auswaehlen.jpg?raw=true)

![](images/zu-bearbeitende-felder-auswaehlen.jpg?raw=true)

![](images/mehrere-datensaetze-bearbeiten.jpg?raw=true)


## Backend-Tastaturkürzel

Um den Workflow bei der Arbeit mit Contao zu beschleunigen, gibt es im Backend
etliche Tastaturkürzel, mit denen sich bestimmte Befehle direkt aufrufen
lassen. Zum Beispiel können Sie die Schaltfläche "Speichern" am Ende eines
Eingabeformulars alternativ zur Bedienung mit der Maus auch mit dem
Tastaturkürzel `[Alt]+[s]` ansteuern.


### Allgemeine Tastaturkürzel

<table>
<tr>
  <th>Tastaturkürzel</th>
  <th>Schaltfläche</th>
  <th>Erklärung</th>
</tr>
<tr>
  <td><code>[Alt]+[h]</code></td>
  <td>Startseite</td>
  <td>Zur Startseite des Backend (<b>H</b>ome).</td>
</tr>
<tr>
  <td><code>[Alt]+[q]</code></td>
  <td>Abmelden</td>
  <td>Beendet die aktuelle Backend-Sitzung (<b>Q</b>uit).</td>
</tr>
<tr>
  <td><code>[Alt]+[t]</code></td>
  <td>Nach oben</td>
  <td>Springt zum Anfang der Seite (<b>T</b>op).</td>
</tr>
<tr>
  <td><code>[Alt]+[b]</code></td>
  <td>Zurück</td>
  <td>Zurück zur vorherigen Seite (<b>B</b>ack).</td>
</tr>
<tr>
  <td><code>[Alt]+[n]</code></td>
  <td>Neuer Datensatz</td>
  <td>Legt einen neuen Datensatz an (<b>N</b>ew).</td>
</tr>
<tr>
  <td><code>[Alt]+[e]</code></td>
  <td>Mehrere bearbeiten</td>
  <td>Wechselt in den "mehrere bearbeiten"-Modus (<b>E</b>dit multiple).</td>
</tr>
<tr>
  <td><code>[Alt]+[f]</code></td>
  <td>Frontend-Vorschau</td>
  <td>Öffnet die Frontend-Vorschau in einem neuen Fenster (<b>F</b>ront end
      preview).</td>
</tr>
</table>


### Tastaturkürzel im Bearbeitungsmodus

<table>
<tr>
  <th>Tastaturkürzel</th>
  <th>Schaltfläche</th>
  <th>Erklärung</th>
</tr>
<tr>
  <td><code>[Alt]+[s]</code></td>
  <td>Speichern</td>
  <td>Speichert das aktuelle Eingabeformular (<b>S</b>ave).</td>
</tr>
<tr>
  <td><code>[Alt]+[c]</code></td>
  <td>Speichern und schließen</td>
  <td>Speichert und schließt das aktuelle Eingabeformular (Save and
      <b>c</b>lose). Sie gelangen zurück zur vorherigen Seite.</td>
</tr>
<tr>
  <td><code>[Alt]+[g]</code></td>
  <td>Speichern und zurück</td>
  <td>Speichert und schließt das aktuelle Eingabeformular (Save and <b>g</b>o
      back). Sie gelangen zurück zur übergeordneten Seite, z.B. von einem
      Inhaltselement direkt zur Artikelübersicht.</td>
</tr>
<tr>
  <td><code>[Alt]+[e]</code></td>
  <td>Speichern und bearbeiten</td>
  <td>Speichert das aktuelle Eingabeformular (Save and <b>e</b>dit) und wechselt
      zur Ansicht der Kind-Datensätze, z.B. beim Anlegen von Stylesheets.</td>
</tr>
<tr>
  <td><code>[Alt]+[n]</code></td>
  <td>Speichern und neu</td>
  <td>Speichert das aktuelle Eingabeformular und legt einen neuen Datensatz an
      (Save and <b>n</b>ew).</td>
</tr>
</table>


### Tastaturkürzel im Modus "mehrere bearbeiten"

<table>
<tr>
  <th>Tastaturkürzel</th>
  <th>Schaltfläche</th>
  <th>Erklärung</th>
</tr>
<tr>
  <td><code>[Alt]+[d]</code></td>
  <td>Mehrere löschen</td>
  <td>Löscht alle ausgewählten Datensätze im Modus »mehrere bearbeiten«
      (<b>D</b>elete).</td>
</tr>
<tr>
  <td><code>[Alt]+[x]</code></td>
  <td>Mehrere verschieben</td>
  <td>Verschiebt alle ausgewählten Datensätze im Modus »mehrere
      bearbeiten«.</td>
</tr>
<tr>
  <td><code>[Alt]+[c]</code></td>
  <td>Mehrere kopieren</td>
  <td>Kopiert alle ausgewählten Datensätze im Modus »mehrere bearbeiten«
      (<b>C</b>opy).</td>
</tr>
<tr>
  <td><code>[Alt]+[v]</code></td>
  <td>Mehrere überschreiben</td>
  <td>Überschreibt alle ausgewählten Datensätze im Modus »mehrere
      bearbeiten«.</td>
</tr>
</table>

Die beschriebenen Tastaturkürzel funktionieren in dieser Form nur unter
Windows. Mac-Nutzer müssen anstatt der `[Alt]`-Taste `[Ctrl]+[⌥ Opt]` in
Verbindung mit dem jeweiligen Kürzel verwenden. Zudem weicht Firefox unter
Windows leider vom gewohnten Standard ab, dort müssen Sie `[Alt]+[Umsch]` in
Verbindung mit dem gewünschten Kürzel drücken.
