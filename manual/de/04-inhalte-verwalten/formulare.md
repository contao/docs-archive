## Formulare

Mit dem Formulargenerator lassen sich interaktive Formulare erstellen, die per
E-Mail verschickt oder in der Datenbank gespeichert werden können. Hochgeladene
Dateien werden als Anhang versendet oder auf dem Server gespeichert. Folgende
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
  <td>Fieldset</td>
  <td>-</td>
  <td>Ein Container für Formularfelder mit einer optionalen Legende.</td>
</tr>
<tr>
  <td>Textfeld</td>
  <td>text</td>
  <td>Ein einzeiliges Eingabefeld für einen kurzen oder mittellangen Text.</td>
</tr>
<tr>
  <td>Passwortfeld</td>
  <td>password</td>
  <td>Ein einzeiliges Eingabefeld für ein Passwort. Contao fügt automatisch
      ein Bestätigungsfeld hinzu.</td>
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
  <td>Eine einfache Rechenaufgabe zur Prüfung ob das Formular von einem
      Menschen abgesendet wurde (CAPTCHA).</td>
</tr>
<tr>
  <td>Absendefeld</td>
  <td>submit</td>
  <td>Eine Absende-Schaltfläche zur Versendung des Formulars.</td>
</tr>
</table>


### Frontend-Modul

Mit dem Frontend-Module des Formulargenerators können Formulare angezeigt werden.
Module können im Backend unter "Layout" -> "Module" konfiguriert werden und
müssen anschließend in einem Artikel oder Seitenlayout eingebunden werden.

<table>
<tr>
  <th>Modul</th>
  <th>CSS-Klasse</th>
  <th>Beschreibung</th>
</tr>
<tr>
  <td>Formular</td>
  <td>mod_form</td>
  <td>Fügt ein Formular auf der Seite ein.</td>
</tr>
</table>


### Inhaltselement

Das Inhaltselement bietet dieselben Funktionen wie das Modul, lässt sich aber
direkt im Artikel einbinden und konfigurieren. Der Formulargenerator
stellt ein Inhaltselement zur Verfügung:

<table>
<tr>
  <th>Inhaltselement</th>
  <th>CSS-Klasse</th>
  <th>Beschreibung</th>
</tr>
<tr>
  <td>Formular</td>
  <td>ce_form</td>
  <td>Fügt ein Formular ein.</td>
</tr>
</table>
