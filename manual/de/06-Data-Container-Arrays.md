# Data Container Arrays

Data Container Arrays (DCAs) dienen zur Speicherung von Tabellen-Metadaten.
Jedes DCA beschreibt die Konfiguration einer bestimmten Tabelle, ihre
Beziehungen zu anderen Tabellen sowie die einzelnen Felder. Die Contao
Core-Engine erkennt anhand dieser Metadaten, wie Datens�tze aufgelistet,
bearbeitet und gespeichert werden. Die DCA-Dateien aller aktiven Module werden
nacheinander geladen (zuerst `backend` und `frontend` und dann in alphabetischer
Reihenfolge) und jedes Modul kann die bestehende Konfiguration �berschreiben.
Die Datei `system/config/dcaconfig.php` wird ganz am Ende eingelesen, so dass
dort �nderungen updatesicher gespeichert werden k�nnen.


## Referenz

Ein Data Container Array ist in 6 Sektionen unterteilt. Die erste Sektion
speichert globale Informationen wie z.B. Relationen zu anderen Tabellen. Die
zweite und dritte Sektion legt fest, wie Datens�tze aufgelistet werden und
welche Aktionen ein Benutzer ausf�hren kann. Die vierte Sektion definiert
verschiedene Gruppen von Eingabefelder (Paletten) und die letzten beiden
Sektionen beschreiben die Eingabefelder im Detail.


### Tabellenkonfiguration

Die Tabellenkonfiguration legt unter anderem fest, welcher Data Container-Typ
verwendet wird oder ob Relationen zu anderen Tabellen bestehen. Sie k�nnen
au�erdem die Versionierung aktivieren und festlegen, was mit Kinddatens�tzen
beim L�schen von Elterndatens�tzen passiert.

<table>
<tr>
  <th>Schl�ssel</th>
  <th>Wert</th>
  <th>Beschreibung</th>
</tr>
<tr>
  <td>label</td>
  <td><code>&amp;$GLOBALS['TL_LANG']</code> (<code>string</code>)</td>
  <td>Die Bezeichnung wird in der Seitenstruktur und in der Dateiverwaltung
      verwendet. Enth�lt normalerweise eine Referenz auf das Spracharray.</td>
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
  <td>closed</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Verbietet das Anlegen neuer Datens�tze in der Tabelle.</td>
</tr>
<tr>
  <td>notEditable</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Verbietet das Bearbeiten der Tabelle.</td>
</tr>
<tr>
  <td>notDeletable</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Verbietet das L�schen von Datens�tzen in der Tabelle.</td>
</tr>
<tr>
  <td>notSortable</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Verbietet das Sortieren von Datens�tzen in der Tabelle.</td>
</tr>
<tr>
  <td>notCopyable</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Verbietet das Kopieren von Datens�tzen in der Tabelle.</td>
</tr>
<tr>
  <td>notCreatable</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Verbietet das erstellen von neuen Datens�tzen (kopieren bleibt erlaubt).</td>
</tr>
<tr>
  <td>switchToEdit</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Aktiviert die "Speichern und Bearbeiten"-Schaltfl�che beim Anlegen eines
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
  <td>Verhindert die Duplizierung der Kinddatens�tze, wenn ein Datensatz der
      Elterntabelle dupliziert wird.</td>
</tr>
<tr>
  <td>doNotDeleteRecords</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Verhindert die L�schung der Kinddatens�tze, wenn ein Datensatz der
      Elterntabelle gel�scht wird.</td>
</tr>
<tr>
  <td>onload_callback</td>
  <td>Callback-Funktion (<code>array</code>)</td>
  <td>Ruft eine Callback-Funktion beim Initialisieren des Data Containers auf
      und �bergibt das DataContainer-Objekt als Argument.
      Der Default Wert f�r einzelne Felder kann hier nicht mehr definiert werden.
      Ebenso ist es nicht mehr m�glich einem Feld dynamisch Optionen (z.B. bei dem InputType "Select") zuzuweisen.
	  Nutzen Sie stattdessen den <code>load_callback</code> bzw. den <code>options_callback</code> des jeweiligen Feldes.</td>
</tr>
<tr>
  <td>onsubmit_callback</td>
  <td>Callback-Funktion (<code>array</code>)</td>
  <td>Ruft eine Callback-Funktion nach der Aktualisierung eines Datensatzes auf
      und �bergibt das DataContainer-Objekt als Argument.</td>
</tr>
<tr>
  <td>ondelete_callback</td>
  <td>Callback-Funktion (<code>array</code>)</td>
  <td>Ruft eine Callback-Funktion beim L�schen eines Datensatzes auf und
      �bergibt das DataContainer-Objekt als Argument.</td>
</tr>
<tr>
  <td>oncut_callback</td>
  <td>Callback-Funktion (<code>array</code>)</td>
  <td>Ruft eine Callback-Funktion beim Verschieben eines Datensatzes auf und
      �bergibt das DataContainer-Objekt als Argument.</td>
</tr>
<tr>
  <td>oncopy_callback</td>
  <td>Callback-Funktion (<code>array</code>)</td>
  <td>Ruft eine Callback-Funktion beim Duplizieren eines Datensatzes auf und
      �bergibt die Insert ID sowie das DataContainer-Objekt als Argument.</td>
</tr>
<tr>
  <td>onversion_callback</td>
  <td>Callback-Funktion (<code>array</code>)</td>
  <td>Ruft eine Callback-Funktion beim Erstellen einer neuen Version eines
      Datensatzes auf und �bergibt die Tabelle, die Insert ID
      sowie das DataContainer-Objekt als Argument.</td>
</tr>
<tr>
  <td>onrestore_callback</td>
  <td>Callback-Funktion (<code>array</code>)</td>
  <td>Ruft eine Callback-Funktion beim Wiederherstellen einer Version eines
      Datensatzes auf und �bergibt die Insert ID, die Tabelle, die Daten sowie
      die Version als Argument.</td>
</tr>
<tr>
  <td>sql</td>
  <td>Tabellen-Konfiguration (<code>array</code>)</td>
  <td>Bestimmt die Konfigurartion der Datenbank-Tabelle, z.B. 
  <code>'keys' => array
  		(
				'id' => 'primary',
				'pid' => 'index'
			)</code></td>
</tr>
</table>


### Datens�tze auflisten

Das Auflistungsarray legt fest, wie Datens�tze aufgelistet werden. Die Contao
Core-Engine unterst�tzt drei [Ansichen][1]: den "List View", den "Parent View"
und den "Tree View". Sie k�nnen verschiedene Filter- und Sortieroptionen setzen
und eigene Bezeichnungen einf�gen.


#### Sortieroptionen

<table>
<tr>
  <th>Schl�ssel</th>
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
      <b>4</b> Darstellung der Kinddatens�tze eines Elterndatensatzes (vgl.
      Stylesheets-Modul)<br>
      <b>5</b> Darstellung als Baum (vgl. Seitenstruktur)<br>
      <b>6</b> Sortierung der Kinddatens�tze anhand eines Baumes (vgl.
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
      <b>sort</b> zeigt das Sortiermen� an<br>
      <b>filter</b> zeigt die Filtermen�s an<br>
      <b>limit</b> zeigt das Limitmen� an. Trennen Sie die Men�s mit Komma
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
  <td>Wurzeldatens�tze (<code>array</code>)</td>
  <td>IDs der Wurzeldatens�tze (Pagemounts). Wird normalerweise automatisch
      gesetzt.</td>
</tr>
<tr>
  <td>filter</td>
  <td>Abfragefilter (<code>array</code>)</td>
  <td>Erm�glicht das Hinzuf�gen eigener Filter als Arrays, z.B.
      <code>array('status=?', 'active')</code>.</td>
</tr>
<tr>
  <td>disableGrouping</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Erm�glicht das Deaktivieren der Gruppen�berschriften im List View und
      Parent View.</td>
</tr>
<tr>
  <td>paste_button_callback</td>
  <td>Callback-Funktion (<code>array</code>)</td>
  <td>Wird anstatt der Standardroutine zur Erstellung der
      Einf�ge-Schaltfl�chen ausgef�hrt.</td>
</tr>
<tr>
  <td>child_record_callback</td>
  <td>Callback-Funktion (<code>array</code>)</td>
  <td>Wird zur Darstellung der Kinddatens�tze ausgef�hrt (nur Sortierungsmodus
      4).</td>
</tr>
<tr>
  <td>child_record_class</td>
  <td>CSS-Klasse (<code>string</code>)</td>
  <td>Erm�glicht das Hinzuf�gen einer CSS-Klasse zu den
      Parent-View-Elementen.</td>
</tr>
</table>


#### Bezeichnungen

<table>
<tr>
  <th>Schl�ssel</th>
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
  <td>Maximale L�nge der Bezeichnung.</td>
</tr>
<tr>
  <td>group_callback</td>
  <td>Callback-Funktion (<code>array</code>)</td>
  <td>Wird anstatt der Standardroutine zur Erstellung der Gruppennamen
      ausgef�hrt.</td>
</tr>
<tr>
  <td>label_callback</td>
  <td>Callback-Funktion (<code>array</code>)</td>
  <td>Wird anstatt der Standardroutine zur Erstellung der Bezeichnung
      ausgef�hrt.</td>
</tr>
</table>


### Aktionen

Das Aktionsarray ist in zwei Bereiche unterteilt: globale Aktionen, die sich auf
die Tabelle beziehen (z.B. mehrere Datens�tze auf einmal bearbeiten), sowie
regul�re Aktionen, die sich auf einen bestimmten Datensatz beziehen (z.B.
Bearbeiten oder L�schen).


#### Globale Aktionen

<table>
<tr>
  <th>Schl�ssel</th>
  <th>Wert</th>
  <th>Beschreibung</th>
</tr>
<tr>
  <td>label</td>
  <td><code>&amp;$GLOBALS['TL_LANG']</code> (<code>string</code>)</td>
  <td>Bezeichnung der Schaltfl�che. Enth�lt normalerweise eine Referenz auf
      das Spracharray.</td>
</tr>
<tr>
  <td>href</td>
  <td>URL-Fragment (<code>string</code>)</td>
  <td>URL-Fragment, das beim Anklicken der Schaltfl�che an die URL angeh�ngt
      wird (z.B. <code>act=editAll</code>).</td>
</tr>
<tr>
  <td>class</td>
  <td>CSS-Klasse (<code>string</code>)</td>
  <td>CSS-Klasse der Schaltfl�che.</td>
</tr>
<tr>
  <td>attributes</td>
  <td>Zus�tzliche Attribute (<code>string</code>)</td>
  <td>Zus�tzliche Attribute wie z.B. Eventhandler oder Style-Definitionen.</td>
</tr>
<tr>
  <td>button_callback</td>
  <td>Callback-Funktion (<code>array</code>)</td>
  <td>Wird anstatt der Standardroutine zur Erstellung des Navigationssymbols
      ausgef�hrt.</td>
</tr>
</table>


#### Regul�re Aktionen

<table>
<tr>
  <th>Schl�ssel</th>
  <th>Wert</th>
  <th>Beschreibung</th>
</tr>
<tr>
  <td>label</td>
  <td><code>&amp;$GLOBALS['TL_LANG']</code> (<code>string</code>)</td>
  <td>Bezeichnung der Schaltfl�che. Enth�lt normalerweise eine Referenz auf
      das Spracharray.</td>
</tr>
<tr>
  <td>href</td>
  <td>URL-Fragment (<code>string</code>)</td>
  <td>URL-Fragment, das beim Anklicken der Schaltfl�che an die URL angeh�ngt
      wird (z.B. <code>act=edit</code>).</td>
</tr>
<tr>
  <td>icon</td>
  <td>Navigationssymbol (<code>string</code>)</td>
  <td>Pfad und Dateiname des Icons.</td>
</tr>
<tr>
  <td>attributes</td>
  <td>Zus�tzliche Attribute (<code>string</code>)</td>
  <td>Zus�tzliche Attribute wie z.B. Eventhandler oder Style-Definitionen.</td>
</tr>
<tr>
  <td>button_callback</td>
  <td>Callback-Funktion (<code>array</code>)</td>
  <td>Wird anstatt der Standardroutine zur Erstellung des Navigationssymbols
      ausgef�hrt.</td>
</tr>
</table>


### Felder

Das Felderarray beschreibt die Spalten einer Tabelle. Anhand dieser Metadaten
entscheidet die Contao Core-Engine, welches Eingabefeld geladen wird, ob ein
Benutzer darauf zugreifen darf und ob es als Sortierkriterium verwendet werden
kann.

<table>
<tr>
  <th>Schl�ssel</th>
  <th>Wert</th>
  <th>Beschreibung</th>
</tr>
<tr>
  <td>label</td>
  <td><code>&amp;$GLOBALS['TL_LANG']</code> (<code>string</code>)</td>
  <td>Bezeichnung des Feldes. Enth�lt normalerweise eine Referenz auf das
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
  <td>Blendet das Feld f�r regul�re Benutzer aus. Kann in den
      Gruppeneinstellungen festgelegt werden (erlaubte Felder).</td>
</tr>
<tr>
  <td>search</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>F�gt das Feld dem Suchmen� hinzu (vgl. "Datens�tze sortieren" ->
      "Paneellayout").</td>
</tr>
<tr>
  <td>sorting</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>F�gt das Feld dem Sortiermen� hinzu (vgl. "Datens�tze sortieren" ->
      "Paneellayout").</td>
</tr>
<tr>
  <td>filter</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>F�gt das Feld dem Filtermen� hinzu (vgl. "Datens�tze sortieren" ->
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
  <td>Sortierl�nge (<code>integer</code>)</td>
  <td>Gibt die Anzahl der Zeichen an, die zur Gruppierung der Datens�tze
      verwendet wird (Sortierflag 3 und 4).</td>
</tr>
<tr>
  <td>inputType</td>
  <td>Feldtyp (<code>string</code>)</td>
  <td><b>text</b> Textfeld<br>
      <b>password</b> Passwortfeld<br>
      <b>textarea</b> Textarea<br>
      <b>select</b> Drop-Down-Men�<br>
      <b>checkbox</b> Checkbox<br>
      <b>radio</b> Radio-Button<br>
      <b>radioTable</b> Tabelle mit Bildern und Radio-Buttons<br>
      <b>inputUnit</b> Textfeld mit Drop-Down-Men� zur Auswahl der Einheit<br>
      <b>trbl</b> Vier Textfelder mit Drop-Down-Men� zur Auswahl der Einheit<br>
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
  <td>Optionen eines Drop-Down- oder Radio-Button-Men�s.</td>
</tr>
<tr>
  <td>options_callback</td>
  <td>Callback-Funktion (<code>array</code>)</td>
  <td>Kann verwendet werden, um die Optionen eines Drow-Down- oder
      Radio-Button-Men�s mit Hilfe einer individuellen Funktion zu laden.</td>
</tr>
<tr>
  <td>foreignKey</td>
  <td>tabelle.feld (<code>string</code>)</td>
  <td>L�dt die Optionen eines Drop-Down- oder Radio-Button-Men�s aus einer
      Tabelle. Verwendet die ID als Schl�ssel und das angegebenen Feld als
      Wert.</td>
</tr>
<tr>
  <td>reference</td>
  <td><code>&amp;$GLOBALS['TL_LANG']</code> (<code>string</code>)</td>
  <td>Bezeichnungen der Optionen. Enth�lt normalerweise eine Referenz auf das
      Spracharray.</td>
</tr>
<tr>
  <td>explanation</td>
  <td><code>&amp;$GLOBALS['TL_LANG']</code> (<code>string</code>)</td>
  <td>Erkl�rung des Feldes. Enth�lt normalerweise eine Referenz auf das
      Spracharray.</td>
</tr>
<tr>
  <td>input_field_callback</td>
  <td>Callback-Funktion (<code>array</code>)</td>
  <td>Wird anstatt der Standardroutine zur Erstellung eines Formularfeldes
      ausgef�hrt und �bergibt das DataContainer-Objekt sowie die Bezeichnung als
      Argument.</td>
</tr>
<tr>
  <td>eval</td>
  <td>Feldkonfiguration (<code>array</code>)</td>
  <td>Verschiedene Einstellungen (vgl. n�chsten Abschnitt).</td>
</tr>
<tr>
  <td>wizard</td>
  <td>Callback-Funktion (<code>array</code>)</td>
  <td>F�gt dem Eingabefeld den R�ckgabewert einer individuellen Funktion
      hinzu.</td>
</tr>
<tr>
  <td>sql</td>
  <td>Tabellenkonfiguration (<code>string</code>)</td>
  <td>Bestimmt den Datentyp und seine Konfiguration in der Datenbank, z.B.
      <code>varchar(255) NOT NULL default ''</code></td>
</tr>
<tr>
  <td>relation</td>
  <td>Relations-Konfiguration (<code>array</code>)</td>
  <td>Bestimmt die Beziehung zur Elterntabelle (vgl. Abschnitt "Relationen").
  </td>
</tr>
<tr>
  <td>load_callback</td>
  <td>Callback-Funktion (<code>array</code>)</td>
  <td>Wird beim Laden des Eingabefeldes ausgef�hrt und �bergibt den Feldwert
      sowie das DataContainer-Objekt als Argument. Erwartet einen Feldwert als
      R�ckgabewert.</td>
</tr>
<tr>
  <td>save_callback</td>
  <td>Callback-Funktion (<code>array</code>)</td>
  <td>Wird beim Speichern des Feldes ausgef�hrt und �bergibt den Feldwert
      sowie das DataContainer-Objekt als Argument. Erwartet einen Feldwert als
      R�ckgabewert. Durch Ausl�sen einer Exception kann eine Fehlermeldung
      ausgegeben werden.</td>
</tr>
</table>


### Evaluation

Das Evaluationsarray konfiguriert ein Eingabefeld im Detail. Sie k�nnen es z.B.
zu einem Pflichtfeld machen,  die verschl�sselte Datenspeicherung aktivieren
oder sein Aussehen ver�ndern. Benutzereingaben k�nnen anhand eines regul�ren
Ausdrucks gepr�ft werden.

<table>
<tr>
  <th>Schl�ssel</th>
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
  <td>Maximale L�nge (<code>integer</code>)</td>
  <td>Legt die maximale Anzahl an Zeichen fest, die in das Feld eingegeben
      werden d�rfen.</td>
</tr>
<tr>
  <td>minlength</td>
  <td>Mindestl�nge (<code>integer</code>)</td>
  <td>Legt die Anzahl an Zeichen fest, die mindestens in das Feld eingegeben
      werden m�ssen.</td>
</tr>
<tr>
  <td>fallback</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Legt fest, dass das Feld nur ein einziges Mal pro Tabelle ausgew�hlt
      werden darf.</td>
</tr>
<tr>
  <td>rgxp</td>
  <td>Regul�rer Ausdruck (<code>string</code>)</td>
  <td>
    <table>
        <tr>
          <td><b>alias</b></td>
          <td>pr�ft auf ein g�ltiges Alias</td>
        </tr>
        <tr>
          <td><b>alnum</b></td>
          <td>erlaubt nur alphanumerische Zeichen (inklusive Punkt [.] 
          Minus [-], Unterstrich [_] und Leerschlag [ ])</td>
        </tr>
        <tr>
          <td><b>alpha</b></td>
          <td>erlaubt nur alphabetische Zeichen (inklusive Punkt [.] 
          Minus [-] und Leerschlag [ ])</td>
        </tr>
        <tr>
          <td><b>date</b></td>
          <td>pr�ft auf ein g�ltiges Datum</td>
        </tr>
        <tr>
          <td><b>datim</b></td>
          <td>pr�ft auf ein g�ltiges Datum mit Uhrzeit</td>
        </tr>
        <tr>
          <td><b>digit</b></td>
          <td>erlaubt nur numerische Zeichen (inklusive Punkt [.] und Minus [-])</td>
        </tr>
        <tr>
          <td><b>email</b></td>
          <td>pr�ft auf eine g�ltige E-Mail-Adresse</td>
        </tr>
        <tr>
          <td><b>emails</b></td>
          <td>pr�ft auf eine Liste von g�ltigen E-Mail-Adressen</td>
        </tr>
        <tr>
          <td><b>extnd</b></td>
          <td>erlaubt alles au�er <code>#&amp;()/&lt;=&gt;</code></td>
        </tr>
        <tr>
          <td><b>friendly</b></td>
          <td>pr�ft auf eine g�ltige E-Mail-Adresse im "friendly name
      format"</td>
        </tr>
        <tr>
          <td><b>language</b></td>
          <td>pr�ft auf einen g�ltigen Sprachcode</td>
        </tr>
        <tr>
          <td><b>locale</b></td>
          <td>pr�ft auf ein g�ltiges Gebietsschema (z.B. "de-CH")</td>
        </tr>
        <tr>
          <td><b>folderalias</b></td>
          <td>pr�ft auf ein g�ltiges Ordner-URL Alias</td>
        </tr>
        <tr>
          <td><b>phone</b></td>
          <td>pr�ft auf eine g�ltige Telefonnummer (Zahlen, Leerschlag [ ], 
          Plus [+], Minus [-], Klammern [()] und Schr�gstrich [/])</td>
        </tr>
        <tr>
          <td><b>prcnt</b></td>
          <td>erlaubt Zahlen zwischen 0 und 100</td>
        </tr>
        <tr>
          <td><b>url</b></td>
          <td>pr�ft auf eine g�ltige URL</td>
        </tr>
        <tr>
          <td><b>time</b></td>
          <td>pr�ft auf eine g�ltige Uhrzeit</td>
        </tr>
    </table>
  </td>
</tr>
<tr>
  <td>cols</td>
  <td>Spalten (<code>integer</code>)</td>
  <td>Anzahl an Spalten (gilt nur f�r Textareas).</td>
</tr>
<tr>
  <td>rows</td>
  <td>Reihen (<code>integer</code>)</td>
  <td>Anzahl an Reihen (gilt nur f�r Textareas).</td>
</tr>
<tr>
  <td>multiple</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Erlaubt die mehrfache Auswahl bzw. Eingabe und kann f�r Textfelder,
      Drop-Down-Men�s, Radio-Buttons und Checkboxen verwendet werden. F�r den
      Checkbox-Assistenten ben�tigt.</td>
</tr>
<tr>
  <td>size</td>
  <td>Gr��e (<code>integer</code>)</td>
  <td>Gr��e eines Mehrfachfeldes bzw. Anzahl an Eingabefeldern.</td>
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
      Die Verwendung eigener Konfigurationsdateien ist m�glich.</td>
</tr>
<tr>
  <td>submitOnChange</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Legt fest, ob das Formular bei der �nderung des Feldwertes automatisch
      abgeschickt wird.</td>
</tr>
<tr>
  <td>nospace</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Legt fest, ob Leerzeichen eingegeben werden d�rfen.</td>
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
      Feldwert nicht ver�ndert wurde.</td>
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
  <td>Speichert den Feldwert verschl�sselt.</td>
</tr>
<tr>
  <td>trailingSlash</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Legt fest, ob dem Feldwert ein Schr�gstrich hinzugef�gt (`true`) oder ein
      bestehender Schr�gstrich am Ende entfernt (`false`) wird.</td>
</tr>
<tr>
  <td>files</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Legt fest, ob Dateien und Ordner oder nur Ordner angezeigt werden. Gilt
      nur f�r Dateib�ume.</td>
</tr>
<tr>
  <td>filesOnly</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Entfernt die Radio Buttons bzw. Checkboxen zur Auswahl von Ordnern. Gilt
      nur f�r Dateib�ume.</td>
</tr>
<tr>
  <td>extensions</td>
  <td>Dateitypen (<code>string</code>)</td>
  <td>Beschr�nkt den Dateibaum auf bestimmte Dateitypen (kommagetrennte Liste).
      Gilt nur f�r Dateib�ume.</td>
</tr>
<tr>
  <td>path</td>
  <td>Pfad (<code>string</code>)</td>
  <td>Individuelles Wurzelverzeichnis f�r Dateib�ume.</td>
</tr>
<tr>
  <td>fieldType</td>
  <td>Feldtyp (<code>string</code>)</td>
  <td><b>checkbox</b> erlaubt die Auswahl mehrerer Dateien<br>
      <b>radio</b> erlaubt die Auswahl genau einer Datei. Gilt nur f�r
      Dateib�ume.</td>
</tr>
<tr>
  <td>includeBlankOption</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Legt fest, ob ein Drop-Down-Men� eine leere Option am Anfang enth�lt.</td>
</tr>
<tr>
  <td>blankOptionLabel</td>
  <td>Label (<code>string</code>)</td>
  <td>Bezeichnung der leeren Option (Standard: <code>-</code>).</td>
</tr>
<tr>
  <td>chosen</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Auswahlmen�s mittels 
      <a href="http://harvesthq.github.io/chosen/" target="_blank">Chosen</a>
      erweitern.</td>
</tr>
<tr>
  <td>findInSet</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Sortiert ein Optionsarray anhand der Schl�ssel anstatt anhand der
      Werte.</td>
</tr>
<tr>
  <td>datepicker</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Aktiviert das Popup zur Auswahl eines Datums.</td>
</tr>
<tr>
  <td>colorpicker</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Aktiviert das Popup zur Farbauswahl.</td>
</tr>
<tr>
  <td>feEditable</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Legt fest, ob ein Feld im Frontend bearbeitet werden darf. Gilt nur f�r
      die Tabelle tl_member.</td>
</tr>
<tr>
  <td>feGroup</td>
  <td>Gruppe (<code>string</code>)</td>
  <td><b>personal</b> Pers�nliche Daten<br>
      <b>address</b> Adressdaten<br>
      <b>contact</b> Kontaktdaten<br>
      <b>login</b> Login-Daten (nur Tabelle <code>tl_member</code>)<br>
      Das Hinzuf�gen eigener Gruppen ist m�glich.</td>
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
      unterst�tzt).</td>
</tr>
<tr>
  <td>readonly</td>
  <td>true/false (<code>boolean</code>)</td>
  <td>Das Feld kann nur gelesen werden (wird nicht von allen Feldern
      unterst�tzt).</td>
</tr>
</table>


### Relationen

Relationen definieren, ob und wie Feldwerte mit einer weiteren
Tabelle zusammen h�ngen. Die referenzierte Tabelle wird im `foreignKey`
Schl�ssel definiert. Relationen erm�glichen den Model-Klassen,
referenzierte Datens�tze effizient und entwicklerfreundlich
zu laden (siehe `Model::getRelated()`).

<table>
<tr>
  <th>Schl�ssel</th>
  <th>Wert</th>
  <th>Beschreibung</th>
</tr>
<tr>
  <td>type</td>
  <td>Beziehungstyp<br> (<code>string</code>)
  <td>
    <b>hasOne</b> Feldwert referenziert einen Kinddatensatz<br>
    <b>hasMany</b> Feldwert referenziert mehrere Kinddatens�tze
       (serialisiert)<br>
    <b>belongsTo</b> Feldwert referenziert eine Elterntabelle
       (z.B. <code>pid</code>)<br>
    <b>belongsToMany</b> Feldwert referenziert mehrere
    Elterndatens�tze (serialisiert)
  </td>
</tr>
<tr>
  <td>load</td>
  <td>Ladeverhalten<br> (<code>string</code>)</td>
  <td>
      <b>lazy</b> L�dt referenzierte Datens�tze erst wenn erforderlich
         (Standard, spart RAM)<br>
      <b>eager</b> L�dt referenzierte Datens�tze automatisch (spart DB-Abfragen)
  </td>
</tr>
</table>


## Paletten

Eine Palette besteht aus mehreren Formularfeldern, die zur Bearbeitung eines
Datensatzes ben�tigt werden. Dabei sind meistens nicht alle Spalten einer
Tabelle enthalten, sondern nur die, die zu einem bestimmten Modul oder Element
geh�ren. Paletten k�nnen sich je nach Benutzerrechten oder Elementtyp
dynamisch �ndern und Teile des Formulars (Subpaletten) k�nnen interaktiv per
Ajax nachgeladen werden.


### Gruppen definieren

Eine Palette ist eine Reihung mehrerer Feldnamen, die durch einen Strichpunkt
(;) oder ein Komma (,) verbunden sind. W�hrend das Komma nur zur Abgrenzung der
Feldnamen verwendet wird, markiert der Strichpunkt den Beginn einer neuen
Gruppe, die aus- und eingeklappt werden kann.

![](images/paletten.jpg?raw=true)

Das obige Beispiel wird durch folgenden Code definiert:

``` {.php}
{title_legend},headline,alias,author;{date_legend},date,time;{teaser_legend:hide},subheadline,teaser
```

Die Platzhalter `title_legend` und `date_legend` werden durch die entsprechenden
�bersetzungen im "TL_LANG"-Array ersetzt.

```
$GLOBALS['TL_LANG']['tl_news']['title_legend'] = 'Titel und Autor';
$GLOBALS['TL_LANG']['tl_news']['date_legend']  = 'Datum und Uhrzeit';
```


### Felder ausrichten

Das Contao-Backend verwendet ein 2-spaltiges Grid-System, um Formularfelder
innerhalb ihrer Gruppen auszurichten. Folgende CSS-Klassen k�nnen in der
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
  <td>Verk�rzt das Eingabefeld, damit genug Platz f�r den Wizard (z.B. Date
      Picker) ist.</td>
</tr>
<tr>
  <td>long</td>
  <td>L�sst das Eingabefeld zwei Spalten umspannen.</td>
</tr>
<tr>
  <td>m12</td>
  <td>F�gt dem Element einen oberen Abstand von 12 Pixeln hinzu (z.B. f�r
      einzelne Checkboxen).</td>
</tr>
</table>


## Callbacks

Callback-Funktionen basieren auf dem Event Dispatcher-Pattern. Sie k�nnen
mehrere Callback-Funktionen pro Ereignis registrieren, die dann bei dessen
Eintreten ausgef�hrt werden. Mit Hilfe von Callbacks kann der Programmablauf
der Contao Core-Engine angepasst werden.


#### Globale Callbacks

<table>
<tr>
  <th>Callback</th>
  <th>Beschreibung</th>
</tr>
<tr>
  <td>onload_callback</td>
  <td>Wird bei der Initialisierung des DataContainer-Objekts ausgef�hrt.
      Erm�glicht z.B. das Pr�fen von Zugriffsrechten oder die dynamische
      �nderung des Data Container Array zur Laufzeit.</td>
</tr>
<tr>
  <td>onsubmit_callback</td>
  <td>Wird beim Abschicken eines Backend-Formulars ausgef�hrt. Erm�glicht z.B.
      die Modifizierung der Formulardaten, bevor diese in die Datenbank
      geschrieben werden (wird in der Kalender-Erweiterung zur
      Intervalberechnung eingesetzt).</td>
</tr>
<tr>
  <td>ondelete_callback</td>
  <td>Wird ausgef�hrt bevor ein Datensatz aus der Datenbank entfernt wird.</td>
</tr>
<tr>
  <td>oncut_callback</td>
  <td>Wird ausgef�hrt nachdem ein Datensatz verschoben wurde.</td>
</tr>
<tr>
  <td>oncopy_callback</td>
  <td>Wird ausgef�hrt nachdem ein Datensatz dupliziert wurde.</td>
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
  <td>Erm�glicht individuelle Einf�ge-Schaltfl�chen und wird z.B. in der
      Seitenstruktur verwenden, um die Icons abh�ngig von den Benutzerrechten zu
      deaktivieren (erfordert eine zus�tzliche Pr�fung mittels
      load_callback).</td>
</tr>
<tr>
  <td>child_record_callback</td>
  <td>Legt fest, wie die Kindelemente im "Parent View" dargestellt werden.</td>
</tr>
<tr>
  <td>group_callback</td>
  <td>Erm�glicht individuelle Gruppennamen in der Listenansicht.</td>
</tr>
<tr>
  <td>label_callback</td>
  <td>Erm�glicht individuelle Bezeichnungen in der Listenansicht und wird z.B.
      im Benutzer-Modul verwendet, um die Status-Icons hinzuzuf�gen.</td>
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
  <td>Erm�glicht individuelle Navigationssymbole und wird z.B. in der
      Seitenstruktur verwenden, um Icons abh�ngig von den Benutzerrechten zu
      deaktivieren (erfordert eine zus�tzliche Pr�fung mittels
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
  <td>Erm�glicht das Bef�llen eines Drop-Down-Men�s oder einer Checkbox-Liste
      mittels einer individuellen Funktion. Kann z.B. f�r bedingte
      Fremdschl�ssel-Relationen verwendet werden.</td>
</tr>
<tr>
  <td>input_field_callback</td>
  <td>Erm�glicht das Erstellen individueller Formularfelder und wird z.B. im
      Backend-Modul "Pers�nliche Daten" verwendet, um das
      "Daten bereinigen"-Feld zu erstellen. Achtung: Eingaben werden nicht
      automatisch gespeichert!</td>
</tr>
<tr>
  <td>load_callback</td>
  <td>Wird bei der Initialisierung eines Formularfeldes ausgef�hrt. Erm�glicht
      z.B. das Laden eines Standardwertes.</td>
</tr>
<tr>
  <td>save_callback</td>
  <td>Wird beim Abschicken eines Feldes ausgef�hrt. Erm�glicht z.B. das
      Hinzuf�gen einer individuellen Pr�fung.</td>
</tr>
</table>


[1]: 02-Administration-area.md#datens%C3%A4tze-auflisten
