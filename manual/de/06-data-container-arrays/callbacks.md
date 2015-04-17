## Callbacks

Callback-Funktionen basieren auf dem Event Dispatcher-Pattern. Sie können
mehrere Callback-Funktionen pro Ereignis registrieren, die dann bei dessen
Eintreten ausgeführt werden. Mit Hilfe von Callbacks kann der Programmablauf
der Contao Core-Engine angepasst werden.


### Globale Callbacks

<table>
<tr>
  <th>Callback</th>
  <th>Beschreibung</th>
</tr>
<tr>
  <td>onload_callback</td>
  <td>Wird bei der Initialisierung des DataContainer-Objekts ausgeführt.
      Ermöglicht z.B. das Prüfen von Zugriffsrechten oder die dynamische
      Änderung des Data Container Arrays zur Laufzeit.</td>
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


### Auflistungscallbacks

<table>
<tr>
  <th>Callback</th>
  <th>Beschreibung</th>
</tr>
<tr>
  <td>paste_button_callback</td>
  <td>Ermöglicht individuelle Einfüge-Schaltflächen und wird z.B. in der
      Seitenstruktur verwendet, um die Icons abhängig von den Benutzerrechten zu
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


### Aktionscallbacks

<table>
<tr>
  <th>Callback</th>
  <th>Beschreibung</th>
</tr>
<tr>
  <td>button_callback</td>
  <td>Ermöglicht individuelle Navigationssymbole und wird z.B. in der
      Seitenstruktur verwendet, um Icons abhängig von den Benutzerrechten zu
      deaktivieren (erfordert eine zusätzliche Prüfung mittels
      load_callback).</td>
</tr>
</table>


### Feldcallbacks

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
