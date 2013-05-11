# Data Container Arrays

Data Container Arrays (DCAs) dienen zur Speicherung von Tabellen-Metadaten.
Jedes DCA beschreibt die Konfiguration einer bestimmten Tabelle, ihre
Beziehungen zu anderen Tabellen sowie die einzelnen Felder. Die Contao
Core-Engine erkennt anhand dieser Metadaten, wie Datensätze aufgelistet,
bearbeitet und gespeichert werden. Die DCA-Dateien aller aktiven Module werden
nacheinander geladen (zuerst `backend` und `frontend` und dann in alphabetischer
Reihenfolge) und jedes Modul kann die bestehende Konfiguration überschreiben.
Die Datei `system/config/dcaconfig.php` wird ganz am Ende eingelesen, so dass
dort Änderungen updatesicher gespeichert werden können.


## Referenz

Ein Data Container Array ist in 6 Sektionen unterteilt. Die erste Sektion
speichert globale Informationen wie z.B. Relationen zu anderen Tabellen. Die
zweite und dritte Sektion legt fest, wie Datensätze aufgelistet werden und
welche Aktionen ein Benutzer ausführen kann. Die vierte Sektion definiert
verschiedene Gruppen von Eingabefelder (Paletten) und die letzten beiden
Sektionen beschreiben die Eingabefelder im Detail.


### Tabellenkonfiguration

Die Tabellenkonfiguration legt unter anderem fest, welcher Data Container-Typ
verwendet wird oder ob Relationen zu anderen Tabellen bestehen. Sie können
außerdem die Versionierung aktivieren und festlegen, was mit Kinddatensätzen
beim Löschen von Elterndatensätzen passiert.

<table>
<tr>
  <th>Schlüssel</th>
  <th>Wert</th>
  <th>Beschreibung</th>
</tr>
<tr>
  <td>label</td>
  <td><code>&$GLOBALS['TL_LANG']</code> (<code>string</code>)</td>
  <td>Die Bezeichnung wird in der Seitenstruktur und in der Dateiverwaltung
      verwendet. Enthält normalerweise eine Referenz auf das Spracharray.</td>
</tr>
<tr>
  <td>ptable</td>
  <td>Elterntabelle (<code>string</code>)</td>
  <td>Name der bezogenen Elterntabelle (table.pid = ptable.id).</td>
</tr>
<tr>
  <td>ctable</td>
  <td>Kindtabellen (<code>array</code>)</td>
  <td>Name der bezogenen Kindtabellen (table.id = ctable.pid).</td>
</tr>
<tr>
  <td>dataContainer</td>
  <td>Data Container (<code>string</code>)</td>
  <td>Table (Tabellen), File (lokale Konfigurationsdatei) oder Folder
      (Dateiverwaltung).</td>
</tr>
<tr>
  <td>validFileTypes</td>
  <td>Dateitypen (<code>string</code>)</td>
  <td>Kommagetrennte Liste gültiger Dateiendungen (nur für Dateibäume).</td>
</tr>
<tr>
  <td>uploadScript</td>
  <td>Dateiname (<code>string</code>)</td>
  <td>Dateiname des FancyUpload-Skripts im Ordner `system/config` (ohne
      Dateiendung).</td>
</tr>
<tr>
  <td>closed</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Verbietet das Anlegen neuer Datensätze in der Tabelle.</td>
</tr>
<tr>
  <td>notEditable</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Verbietet das Bearbeiten der Tabelle.</td>
</tr>
<tr>
  <td>switchToEdit</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Aktiviert die "Speichern und Bearbeiten"-Schaltfläche beim Anlegen eines
      neuen Datensatzes (nur Sortierungsmodus 4).</td>
</tr>
<tr>
  <td>enableVersioning</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Aktiviert das Anlegen einer neuen Version beim Speichern eines
      Datensatzes.</td>
</tr>
<tr>
  <td>doNotCopyRecords</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Verhindert die Duplizierung der Kinddatensätze, wenn ein Datensatz der
      Elterntabelle dupliziert wird.</td>
</tr>
<tr>
  <td>doNotDeleteRecords</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Verhindert die Löschung der Kinddatensätze, wenn ein Datensatz der
      Elterntabelle gelöscht wird.</td>
</tr>
<tr>
  <td>onload_callback</td>
  <td>Callback-Funktion (<code>array</code>)</td>
  <td>Ruft eine Callback-Funktion beim Initialisieren des Data Containers auf
      und übergibt das DataContainer-Objekt als Argument.</td>
</tr>
<tr>
  <td>onsubmit_callback</td>
  <td>Callback-Funktion (<code>array</code>)</td>
  <td>Ruft eine Callback-Funktion nach der Aktualisierung eines Datensatzes auf
      und übergibt das DataContainer-Objekt als Argument.</td>
</tr>
<tr>
  <td>ondelete_callback</td>
  <td>Callback-Funktion (<code>array</code>)</td>
  <td>Ruft eine Callback-Funktion beim Löschen eines Datensatzes auf und
      übergibt das DataContainer-Objekt als Argument.</td>
</tr>
<tr>
  <td>oncut_callback</td>
  <td>Callback-Funktion (<code>array</code>)</td>
  <td>Ruft eine Callback-Funktion beim Verschieben eines Datensatzes auf und
      übergibt das DataContainer-Objekt als Argument.</td>
</tr>
<tr>
  <td>oncopy_callback</td>
  <td>Callback-Funktion (<code>array</code>)</td>
  <td>Ruft eine Callback-Funktion beim Duplizieren eines Datensatzes auf und
      übergibt die Insert ID sowie das DataContainer-Objekt als Argument.</td>
</tr>
</table>


### Datensätze auflisten

Das Auflistungsarray legt fest, wie Datensätze aufgelistet werden. Die Contao
Core-Engine unterstützt drei [Ansichen][1]: den "List View", den "Parent View"
und den "Tree View". Sie können verschiedene Filter- und Sortieroptionen setzen
und eigene Bezeichnungen einfügen.


#### Sortieroptionen

<table>
<tr>
  <th>Schlüssel</th>
  <th>Wert</th>
  <th>Beschreibung</th>
</tr>
<tr>
  <td>mode</td>
  <td>Sortierungsmodus (<code>integer</code>)</td>
  <td><b>0</b> Keine Sortierung<br>
      <b>1</b> Sortierung nach einem festen Feld<br>
      <b>2</b> Sortierung nach einem variablen Feld<br>
      <b>3</b> Sortierung anhand der Elterntabelle<br>
      <b>4</b> Darstellung der Kinddatensätze eines Elterndatensatzes (vgl.
      Stylesheets-Modul)<br>
      <b>5</b> Darstellung als Baum (vgl. Seitenstruktur)<br>
      <b>6</b> Sortierung der Kinddatensätze anhand eines Baumes (vgl.
      Artikelverwaltung)</td>
</tr>
<tr>
  <td>flag</td>
  <td>Sortierflag (<code>integer</code>)</td>
  <td><b>1</b> Aufsteigende Sortierung nach Anfangsbuchstabe<br>
      <b>2</b> Absteigende Sortierung nach Anfangsbuchstabe<br>
      <b>3</b> Aufsteigende Sortierung nach den ersten beiden Buchstaben<br>
      <b>4</b> Absteigende Sortierung nach den ersten beiden Buchstaben<br>
      <b>5</b> Aufsteigende Sortierung nach Tag<br>
      <b>6</b> Absteigende Sortierung nach Tag<br>
      <b>7</b> Aufsteigende Sortierung nach Monat<br>
      <b>8</b> Absteigende Sortierung nach Monat<br>
      <b>9</b> Aufsteigende Sortierung nach Jahr<br>
      <b>10</b> Absteigende Sortierung nach Jahr<br>
      <b>11</b> Aufsteigende Sortierung<br>
      <b>12</b> Absteigende Sortierung</td>
</tr>
<tr>
  <td>panelLayout</td>
  <td>Paneellayout (<code>string</code>)</td>
  <td><b>search</b> zeigt das Suchfeld an<br>
      <b>sort</b> zeigt das Sortiermenü an<br>
      <b>filter</b> zeigt die Filtermenüs an<br>
      <b>limit</b> zeigt das Limitmenü an. Trennen Sie die Menüs mit Komma
      (= Abstand) oder Strichpunkt (= neue Zeile), also z.B. 
      <code>sort,filter;search,limit</code>.</td>
</tr>
<tr>
  <td>fields</td>
  <td>Standard-Sortierfelder (<code>array</code>)</td>
  <td>Eines oder mehrere Felder, anhand derer die Tabelle sortiert wird.</td>
</tr>
<tr>
  <td>headerFields</td>
  <td>Header-Felder (<code>array</code>)</td>
  <td>Eines oder mehrere Felder, die im Header des Parent View angezeigt werden
      (nur Sortierungsmodus 4).</td>
</tr>
<tr>
  <td>icon</td>
  <td>Baumsymbole (<code>string</code>)</td>
  <td>Pfad zu einem Symbol, das oberhalb des Baumes angezeigt wird (nur
      Sortierungsmodus 5 und 6).</td>
</tr>
<tr>
  <td>root</td>
  <td>Wurzeldatensätze (<code>array</code>)</td>
  <td>IDs der Wurzeldatensätze (Pagemounts). Wird normalerweise automatisch
      gesetzt.</td>
</tr>
<tr>
  <td>filter</td>
  <td>Abfragefilter (<code>array</code>)</td>
  <td>Ermöglicht das Hinzufügen eigener Filter als Arrays, z.B.
      <code>array('status=?', 'active')</code>.</td>
</tr>
<tr>
  <td>disableGrouping</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Ermöglicht das Deaktivieren der Gruppenüberschriften im List View und
      Parent View.</td>
</tr>
<tr>
  <td>paste_button_callback</td>
  <td>Callback-Funktion (<code>array</code>)</td>
  <td>Wird anstatt der Standardroutine zur Erstellung der
      Einfüge-Schaltflächen ausgeführt.</td>
</tr>
<tr>
  <td>child_record_callback</td>
  <td>Callback-Funktion (<code>array</code>)</td>
  <td>Wird zur Darstellung der Kinddatensätze ausgeführt (nur Sortierungsmodus
      4).</td>
</tr>
<tr>
  <td>child_record_class</td>
  <td>CSS-Klasse (<code>string</code>)</td>
  <td>Ermöglicht das Hinzufügen einer CSS-Klasse zu den
      Parent-View-Elementen.</td>
</tr>
</table>


#### Bezeichnungen

<table>
<tr>
  <th>Schlüssel</th>
  <th>Wert</th>
  <th>Beschreibung</th>
</tr>
<tr>
  <td>fields</td>
  <td>Felder (<code>array</code>)</td>
  <td>Eines oder mehrere Felder, die in der Liste angezeigt werden.</td>
</tr>
<tr>
  <td>format</td>
  <td>Format-String (<code>string</code>)</td>
  <td>HTML-Zeichenkette zur Formatierung der angezeigten Felder (z.B.
      <code>%s</code>).</td>
</tr>
<tr>
  <td>maxCharacters</td>
  <td>Anzahl an Zeichen (<code>integer</code>)</td>
  <td>Maximale Länge der Bezeichnung.</td>
</tr>
<tr>
  <td>group_callback</td>
  <td>Callback-Funktion (<code>array</code>)</td>
  <td>Wird anstatt der Standardroutine zur Erstellung der Gruppennamen
      ausgeführt.</td>
</tr>
<tr>
  <td>label_callback</td>
  <td>Callback-Funktion (<code>array</code>)</td>
  <td>Wird anstatt der Standardroutine zur Erstellung der Bezeichnung
      ausgeführt.</td>
</tr>
</table>


### Aktionen

Das Aktionsarray ist in zwei Bereiche unterteilt: globale Aktionen, die sich auf
die Tabelle beziehen (z.B. mehrere Datensätze auf einmal bearbeiten), sowie
reguläre Aktionen, die sich auf einen bestimmten Datensatz beziehen (z.B.
Bearbeiten oder Löschen).


#### Globale Aktionen

<table>
<tr>
  <th>Schlüssel</th>
  <th>Wert</th>
  <th>Beschreibung</th>
</tr>
<tr>
  <td>label</td>
  <td><code>&$GLOBALS['TL_LANG']</code> (<code>string</code>)</td>
  <td>Bezeichnung der Schaltfläche. Enthält normalerweise eine Referenz auf
      das Spracharray.</td>
</tr>
<tr>
  <td>href</td>
  <td>URL-Fragment (<code>string</code>)</td>
  <td>URL-Fragment, das beim Anklicken der Schaltfläche an die URL angehängt
      wird (z.B. <code>act=editAll</code>).</td>
</tr>
<tr>
  <td>class</td>
  <td>CSS-Klasse (<code>string</code>)</td>
  <td>CSS-Klasse der Schaltfläche.</td>
</tr>
<tr>
  <td>attributes</td>
  <td>Zusätzliche Attribute (<code>string</code>)</td>
  <td>Zusätzliche Attribute wie z.B. Eventhandler oder Style-Definitionen.</td>
</tr>
<tr>
  <td>button_callback</td>
  <td>Callback-Funktion (<code>array</code>)</td>
  <td>Wird anstatt der Standardroutine zur Erstellung des Navigationssymbols
      ausgeführt.</td>
</tr>
</table>


#### Reguläre Aktionen

<table>
<tr>
  <th>Schlüssel</th>
  <th>Wert</th>
  <th>Beschreibung</th>
</tr>
<tr>
  <td>label</td>
  <td><code>&$GLOBALS['TL_LANG']</code> (<code>string</code>)</td>
  <td>Bezeichnung der Schaltfläche. Enthält normalerweise eine Referenz auf
      das Spracharray.</td>
</tr>
<tr>
  <td>href</td>
  <td>URL-Fragment (<code>string</code>)</td>
  <td>URL-Fragment, das beim Anklicken der Schaltfläche an die URL angehängt
      wird (z.B. <code>act=edit</code>).</td>
</tr>
<tr>
  <td>icon</td>
  <td>Navigationssymbol (<code>string</code>)</td>
  <td>Pfad und Dateiname des Icons.</td>
</tr>
<tr>
  <td>attributes</td>
  <td>Zusätzliche Attribute (<code>string</code>)</td>
  <td>Zusätzliche Attribute wie z.B. Eventhandler oder Style-Definitionen.</td>
</tr>
<tr>
  <td>button_callback</td>
  <td>Callback-Funktion (<code>array</code>)</td>
  <td>Wird anstatt der Standardroutine zur Erstellung des Navigationssymbols
      ausgeführt.</td>
</tr>
</table>


### Felder

Das Felderarray beschreibt die Spalten einer Tabelle. Anhand dieser Metadaten
entscheidet die Contao Core-Engine, welches Eingabefeld geladen wird, ob ein
Benutzer darauf zugreifen darf und ob es als Sortierkriterium verwendet werden
kann.

<table>
<tr>
  <th>Schlüssel</th>
  <th>Wert</th>
  <th>Beschreibung</th>
</tr>
<tr>
  <td>label</td>
  <td><code>&$GLOBALS['TL_LANG']</code> (<code>string</code>)</td>
  <td>Bezeichnung des Feldes. Enthält normalerweise eine Referenz auf das
      Spracharray.</td>
</tr>
<tr>
  <td>default</td>
  <td>Standardwert (<code>mixed</code>)</td>
  <td>Der Standardwert wird bei der Erstellung eines neuen Datensatzes
      gesetzt.</td>
</tr>
<tr>
  <td>exclude</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Blendet das Feld für reguläre Benutzer aus. Kann in den
      Gruppeneinstellungen festgelegt werden (erlaubte Felder).</td>
</tr>
<tr>
  <td>search</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Fügt das Feld dem Suchmenü hinzu (vgl. "Datensätze sortieren" ->
      "Paneellayout").</td>
</tr>
<tr>
  <td>sorting</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Fügt das Feld dem Sortiermenü hinzu (vgl. "Datensätze sortieren" ->
      "Paneellayout").</td>
</tr>
<tr>
  <td>filter</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Fügt das Feld dem Filtermenü hinzu (vgl. "Datensätze sortieren" ->
      "Paneellayout").</td>
</tr>
<tr>
  <td>flag</td>
  <td>Sortierflag (<code>integer</code>)</td>
  <td><b>1</b> Aufsteigende Sortierung nach Anfangsbuchstabe<br>
      <b>2</b> Absteigende Sortierung nach Anfangsbuchstabe<br>
      <b>3</b> Aufsteigende Sortierung nach den ersten X Buchstaben (vgl.
      length)<br>
      <b>4</b> Absteigende Sortierung nach den ersten X Buchstaben (vgl.
      length)<br>
      <b>5</b> Aufsteigende Sortierung nach Tag<br>
      <b>6</b> Absteigende Sortierung nach Tag<br>
      <b>7</b> Aufsteigende Sortierung nach Monat<br>
      <b>8</b> Absteigende Sortierung nach Monat<br>
      <b>9</b> Aufsteigende Sortierung nach Jahr<br>
      <b>10</b> Absteigende Sortierung nach Jahr<br>
      <b>11</b> Aufsteigende Sortierung<br>
      <b>12</b> Absteigende Sortierung</td>
</tr>
<tr>
  <td>length</td>
  <td>Sortierlänge (<code>integer</code>)</td>
  <td>Gibt die Anzahl der Zeichen an, die zur Gruppierung der Datensätze
      verwendet wird (Sortierflag 3 und 4).</td>
</tr>
<tr>
  <td>inputType</td>
  <td>Feldtyp (<code>string</code>)</td>
  <td><b>text</b> Textfeld<br>
      <b>password</b> Passwortfeld<br>
      <b>textarea</b> Textarea<br>
      <b>select</b> Drop-Down-Menü<br>
      <b>checkbox</b> Checkbox<br>
      <b>radio</b> Radio-Button<br>
      <b>radioTable</b> Tabelle mit Bildern und Radio-Buttons<br>
      <b>inputUnit</b> Textfeld mit Drop-Down-Menü zur Auswahl der Einheit<br>
      <b>trbl</b> Vier Textfelder mit Drop-Down-Menü zur Auswahl der Einheit<br>
      <b>chmod</b> CHMOD-Tabelle<br>
      <b>pageTree</b> Seitenbaum<br>
      <b>fileTree</b> Dateibaum<br>
      <b>tableWizard</b> Tabellenassistent<br>
      <b>listWizard</b> Listenassistent<br>
      <b>optionWizard</b> Optionsassistent<br>
      <b>moduleWizard</b> Modulassistent<br>
      <b>checkboxWizard</b> Checkbox-Assistent</td>
</tr>
<tr>
  <td>options</td>
  <td>Optionen (<code>array</code>)</td>
  <td>Optionen eines Drop-Down- oder Radio-Button-Menüs.</td>
</tr>
<tr>
  <td>options_callback</td>
  <td>Callback-Funktion (<code>array</code>)</td>
  <td>Kann verwendet werden, um die Optionen eines Drow-Down- oder
      Radio-Button-Menüs mit Hilfe einer individuellen Funktion zu laden.</td>
</tr>
<tr>
  <td>foreignKey</td>
  <td>tabelle.feld (<code>string</code>)</td>
  <td>Lädt die Optionen eines Drop-Down- oder Radio-Button-Menüs aus einer
      Tabelle. Verwendet die ID als Schlüssel und das angegebenen Feld als
      Wert.</td>
</tr>
<tr>
  <td>reference</td>
  <td><code>&$GLOBALS['TL_LANG']</code> (<code>string</code>)</td>
  <td>Bezeichnungen der Optionen. Enthält normalerweise eine Referenz auf das
      Spracharray.</td>
</tr>
<tr>
  <td>explanation</td>
  <td><code>&$GLOBALS['TL_LANG']</code> (<code>string</code>)</td>
  <td>Erklärung des Feldes. Enthält normalerweise eine Referenz auf das
      Spracharray.</td>
</tr>
<tr>
  <td>input_field_callback</td>
  <td>Callback-Funktion (<code>array</code>)</td>
  <td>Wird anstatt der Standardroutine zur Erstellung eines Formularfeldes
      ausgeführt und übergibt das DataContainer-Objekt sowie die Bezeichnung als
      Argument.</td>
</tr>
<tr>
  <td>eval</td>
  <td>Feldkonfiguration (<code>array</code>)</td>
  <td>Verschiedene Einstellungen (vgl. nächsten Abschnitt).</td>
</tr>
<tr>
  <td>wizard</td>
  <td>Callback-Funktion (<code>array</code>)</td>
  <td>Fügt dem Eingabefeld den Rückgabewert einer individuellen Funktion
      hinzu.</td>
</tr>
<tr>
  <td>sql</td>
  <td>Feldkonfiguration (<code>string</code>)</td>
  <td>Bestimmt den Datentyp und seine Konfiguration in der Datenbank, z.B.
      'sql' =>  "varchar(255) NOT NULL default ''"</td>
<tr>
  <td>load_callback</td>
  <td>Callback-Funktion (<code>array</code>)</td>
  <td>Wird beim Laden des Eingabefeldes ausgeführt und übergibt den Feldwert
      sowie das DataContainer-Objekt als Argument. Erwartet einen Feldwert als
      Rückgabewert.</td>
</tr>
<tr>
  <td>save_callback</td>
  <td>Callback-Funktion (<code>array</code>)</td>
  <td>Wird beim Speichern des Feldes ausgeführt und übergibt den Feldwert
      sowie das DataContainer-Objekt als Argument. Erwartet einen Feldwert als
      Rückgabewert. Durch Auslösen einer Exception kann eine Fehlermeldung
      ausgegeben werden.</td>
</tr>
</table>


### Evaluation

Das Evaluationsarray konfiguriert ein Eingabefeld im Detail. Sie können es z.B.
zu einem Pflichtfeld machen,  die verschlüsselte Datenspeicherung aktivieren
oder sein Aussehen verändern. Benutzereingaben können anhand eines regulären
Ausdrucks geprüft werden.

<table>
<tr>
  <th>Schlüssel</th>
  <th>Wert</th>
  <th>Beschreibung</th>
</tr>
<tr>
  <td>helpwizard</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Zeigt das Icon zum Aufruf des Hilfeassistenten neben der Feldbezeichnung
      an.</td>
</tr>
<tr>
  <td>mandatory</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Macht ein Feld zu einem Pflichtfeld.</td>
</tr>
<tr>
  <td>maxlength</td>
  <td>Maximale Länge (<code>integer</code>)</td>
  <td>Legt die maximale Anzahl an Zeichen fest, die in das Feld eingegeben
      werden dürfen.</td>
</tr>
<tr>
  <td>minlength</td>
  <td>Mindestlänge (<code>integer</code>)</td>
  <td>Legt die Anzahl an Zeichen fest, die mindestens in das Feld eingegeben
      werden müssen.</td>
</tr>
<tr>
  <td>fallback</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Legt fest, dass das Feld nur ein einziges Mal pro Tabelle ausgewählt
      werden darf.</td>
</tr>
<tr>
  <td>rgxp</td>
  <td>Regulärer Ausdruck (<code>string</code>)</td>
  <td><b>digit</b> erlaubt nur numerische Zeichen<br>
      <b>alpha</b> erlaubt nur alphabetische Zeichen<br>
      <b>alnum</b> erlaubt nur alphanumerische Zeichen<br>
      <b>extnd</b> erlaubt alles außer <code>#&amp;()/<=></code><br>
      <b>prcnt</b> erlaubt Zahlen zwischen 0 und 100<br>
      <b>date</b> prüft auf ein gültiges Datum<br>
      <b>time</b> prüft auf eine gültige Uhrzeit<br>
      <b>datim</b> prüft auf ein gültiges Datum mit Uhrzeit<br>
      <b>email</b> prüft auf eine gültige E-Mail-Adresse<br>
      <b>friendly</b> prüft auf eine gültige E-Mail-Adresse im "friendly name
      format"<br>
      <b>url</b> prüft auf eine gültige URL<br>
      <b>phone</b> prüft auf eine gültige Telefonnummer</td>
</tr>
<tr>
  <td>cols</td>
  <td>Spalten (<code>integer</code>)</td>
  <td>Anzahl an Spalten (gilt nur für Textareas).</td>
</tr>
<tr>
  <td>rows</td>
  <td>Reihen (<code>integer</code>)</td>
  <td>Anzahl an Reihen (gilt nur für Textareas).</td>
</tr>
<tr>
  <td>wrap</td>
  <td>Zeilenumbruch (<code>string</code>)</td>
  <td><b>off</b> Zeilenumbruch ausschalten<br>
      <b>soft</b> Weicher Zeilenumbruch<br>
      <b>hard</b> Harter Zeilenumbruch</td>
</tr>
<tr>
  <td>multiple</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Erlaubt die mehrfache Auswahl bzw. Eingabe und kann für Textfelder,
      Drop-Down-Menüs, Radio-Buttons und Checkboxen verwendet werden. Für den
      Checkbox-Assistenten benötigt.</td>
</tr>
<tr>
  <td>size</td>
  <td>Größe (<code>integer</code>)</td>
  <td>Größe eines Mehrfachfeldes bzw. Anzahl an Eingabefeldern.</td>
</tr>
<tr>
  <td>style</td>
  <td>Formatierung (<code>string</code>)</td>
  <td>CSS-Formatierung (z.B. <code>border:2px</code>)</td>
</tr>
<tr>
  <td>rte</td>
  <td>Rich Text Editor-Datei (<code>string</code>)</td>
  <td><b>tinyMCE</b> Konfigurationsdatei <code>config/tinyMCE.php</code>
      verwenden<br>
      <b>tinyFlash</b> Konfigurationsdatei <code>config/tinyFlash.php</code>
      verwenden<br>
      Die Verwendung eigener Konfigurationsdateien ist möglich.</td>
</tr>
<tr>
  <td>submitOnChange</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Legt fest, ob das Formular bei der Änderung des Feldwertes automatisch
      abgeschickt wird.</td>
</tr>
<tr>
  <td>nospace</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Legt fest, ob Leerzeichen eingegeben werden dürfen.</td>
</tr>
<tr>
  <td>allowHtml</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Legt fest, ob HTML-Eingaben erlaubt sind.</td>
</tr>
<tr>
  <td>preserveTags</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Erlaubt alle (!) HTML-Tags in Benutzereingaben.</td>
</tr>
<tr>
  <td>decodeEntities</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Legt fest, ob HTML-Entities dekodiert werden (immer der Fall bei
      HTML-Eingaben).</td>
</tr>
<tr>
  <td>doNotSaveEmpty</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Verhindert das Speichern des leeren Feldes.</td>
</tr>
<tr>
  <td>alwaysSave</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Legt fest, dass Eingaben immer gespeichert werden, selbst wenn der
      Feldwert nicht verändert wurde.</td>
</tr>
<tr>
  <td>spaceToUnderscore</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Wandelt alle Leerzeichen in Unterstriche um.</td>
</tr>
<tr>
  <td>unique</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Legt fest, dass ein Feldwert nur einmal vorkommen darf.</td>
</tr>
<tr>
  <td>encrypt</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Speichert den Feldwert verschlüsselt.</td>
</tr>
<tr>
  <td>trailingSlash</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Legt fest, ob dem Feldwert ein Schrägstrich hinzugefügt (`true`) oder ein
      bestehender Schrägstrich am Ende entfernt (`false`) wird.</td>
</tr>
<tr>
  <td>files</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Legt fest, ob Dateien und Ordner oder nur Ordner angezeigt werden. Gilt
      nur für Dateibäume.</td>
</tr>
<tr>
  <td>filesOnly</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Entfernt die Radio Buttons bzw. Checkboxen zur Auswahl von Ordnern. Gilt
      nur für Dateibäume.</td>
</tr>
<tr>
  <td>extensions</td>
  <td>Dateitypen (<code>string</code>)</td>
  <td>Beschränkt den Dateibaum auf bestimmte Dateitypen (kommagetrennte Liste).
      Gilt nur für Dateibäume.</td>
</tr>
<tr>
  <td>path</td>
  <td>Pfad (<code>string</code>)</td>
  <td>Individuelles Wurzelverzeichnis für Dateibäume.</td>
</tr>
<tr>
  <td>fieldType</td>
  <td>Feldtyp (<code>string</code>)</td>
  <td><b>checkbox</b> erlaubt die Auswahl mehrerer Dateien<br>
      <b>radio</b> erlaubt die Auswahl genau einer Datei. Gilt nur für
      Dateibäume.</td>
</tr>
<tr>
  <td>includeBlankOption</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Legt fest, ob ein Drop-Down-Menü eine leere Option am Anfang enthält.</td>
</tr>
<tr>
  <td>blankOptionLabel</td>
  <td>Label (<code>string</code>)</td>
  <td>Bezeichnung der leeren Option (Standard: <code>-</code>).</td>
</tr>
<tr>
  <td>findInSet</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Sortiert ein Optionsarray anhand der Schlüssel anstatt anhand der
      Werte.</td>
</tr>
<tr>
  <td>datepicker</td>
  <td>Date-Picker (<code>string</code>)</td>
  <td>Konfiguration des Assistenten zur Datumsauswahl.</td>
</tr>
<tr>
  <td>feEditable</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Legt fest, ob ein Feld im Frontend bearbeitet werden darf. Gilt nur für
      die Tabelle tl_member.</td>
</tr>
<tr>
  <td>feGroup</td>
  <td>Gruppe (<code>string</code>)</td>
  <td><b>personal</b> Persönliche Daten<br>
      <b>address</b> Adressdaten<br>
      <b>contact</b> Kontaktdaten<br>
      <b>login</b> Login-Daten (nur Tabelle <code>tl_member</code>)<br>
      Das Hinzufügen eigener Gruppen ist möglich.</td>
</tr>
<tr>
  <td>feViewable</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Legt fest, ob das Feld in der Mitgliederliste sichtbar ist.</td>
</tr>
<tr>
  <td>doNotCopy</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Legt fest, dass das Feld beim Duplizieren des Datensatzes nicht mit
      kopiert wird.</td>
</tr>
<tr>
  <td>hideInput</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Versteckt den Inhalt des Feldes (dieser ist jedoch trotzdem im Quelltext
      sichtbar!).</td>
</tr>
<tr>
  <td>doNotShow</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Versteckt das Feld in der "Mehrere bearbeiten"- und "Details
      anzeigen"-Ansicht.</td>
</tr>
<tr>
  <td>isBoolean</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Zeigt an, dass das Feld vom Typ Boolean ist.</td>
</tr>
<tr>
  <td>disabled</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Deaktiviert das Eingabefeld (wird nicht von allen Feldern
      unterstützt).</td>
</tr>
<tr>
  <td>readonly</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Das Feld kann nur gelesen werden (wird nicht von allen Feldern
      unterstützt).</td>
</tr>
</table>


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

![](https://raw.github.com/contao/docs/3.1/manual/de/images/paletten.jpg)

Das obige Beispiel wird durch folgenden Code definiert:

``` {.php}
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
  <td>Hebt alle Floats auf.</td>
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


## Callbacks

Callback-Funktionen basieren auf dem Event Dispatcher-Pattern. Sie können
mehrere Callback-Funktionen pro Ereignis registrieren, die dann bei dessen
Eintreten ausgeführt werden. Mit Hilfe von Callbacks kann der Programmablauf
der Contao Core-Engine angepasst werden.


#### Globale Callbacks

<table>
<tr>
  <th>Callback</th>
  <th>Beschreibung</th>
</tr>
<tr>
  <td>onload_callback</td>
  <td>Wird bei der Initialisierung des DataContainer-Objekts ausgeführt.
      Ermöglicht z.B. das Prüfen von Zugriffsrechten oder die dynamische
      Änderung des Data Container Array zur Laufzeit.</td>
</tr>
<tr>
  <td>onsubmit_callback</td>
  <td>Wird beim Abschicken eines Backend-Formulars ausgeführt. Ermöglicht z.B.
      die Modifizierung der Formulardaten, bevor diese in die Datenbank
      geschrieben werden (wird in der Kalender-Erweiterung zur
      Intervalberechnung eingesetzt).</td>
</tr>
<tr>
  <td>ondelete_callback</td>
  <td>Wird ausgeführt bevor ein Datensatz aus der Datenbank entfernt wird.</td>
</tr>
<tr>
  <td>oncut_callback</td>
  <td>Wird ausgeführt nachdem ein Datensatz verschoben wurde.</td>
</tr>
<tr>
  <td>oncopy_callback</td>
  <td>Wird ausgeführt nachdem ein Datensatz dupliziert wurde.</td>
</tr>
</table>


#### Auflistungscallbacks

<table>
<tr>
  <th>Callback</th>
  <th>Beschreibung</th>
</tr>
<tr>
  <td>paste_button_callback</td>
  <td>Ermöglicht individuelle Einfüge-Schaltflächen und wird z.B. in der
      Seitenstruktur verwenden, um die Icons abhängig von den Benutzerrechten zu
      deaktivieren (erfordert eine zusätzliche Prüfung mittels
      load_callback).</td>
</tr>
<tr>
  <td>child_record_callback</td>
  <td>Legt fest, wie die Kindelemente im "Parent View" dargestellt werden.</td>
</tr>
<tr>
  <td>group_callback</td>
  <td>Ermöglicht individuelle Gruppennamen in der Listenansicht.</td>
</tr>
<tr>
  <td>label_callback</td>
  <td>Ermöglicht individuelle Bezeichnungen in der Listenansicht und wird z.B.
      im Benutzer-Modul verwendet, um die Status-Icons hinzuzufügen.</td>
</tr>
</table>


#### Aktionscallbacks

<table>
<tr>
  <th>Callback</th>
  <th>Beschreibung</th>
</tr>
<tr>
  <td>button_callback</td>
  <td>Ermöglicht individuelle Navigationssymbole und wird z.B. in der
      Seitenstruktur verwenden, um Icons abhängig von den Benutzerrechten zu
      deaktivieren (erfordert eine zusätzliche Prüfung mittels
      load_callback).</td>
</tr>
</table>


#### Feldcallbacks

<table>
<tr>
  <th>Callback</th>
  <th>Beschreibung</th>
</tr>
<tr>
  <td>options_callback</td>
  <td>Ermöglicht das Befüllen eines Drop-Down-Menüs oder einer Checkbox-Liste
      mittels einer individuellen Funktion. Kann z.B. für bedingte
      Fremdschlüssel-Relationen verwendet werden.</td>
</tr>
<tr>
  <td>input_field_callback</td>
  <td>Ermöglicht das Erstellen individueller Formularfelder und wird z.B. im
      Backend-Modul "Persönliche Daten" verwendet, um das
      "Daten bereinigen"-Feld zu erstellen. Achtung: Eingaben werden nicht
      automatisch gespeichert!</td>
</tr>
<tr>
  <td>load_callback</td>
  <td>Wird bei der Initialisierung eines Formularfeldes ausgeführt. Ermöglicht
      z.B. das Laden eines Standardwertes.</td>
</tr>
<tr>
  <td>save_callback</td>
  <td>Wird beim Abschicken eines Feldes ausgeführt. Ermöglicht z.B. das
      Hinzufügen einer individuellen Prüfung.</td>
</tr>
</table>


[1]: 02-Administration-area.md#datens%C3%A4tze-auflisten
