# Das Extension Repository

Um eine Erweiterung im Extension Repository zu veröffentlichen, benötigen Sie
ein [Benutzerkonto][1]. Nach der Anmeldung können Sie über die beiden Links
"Erweiterungen verwalten" und "Übersetzungen verwalten" im [Extension
Repository][2] auf das Entwickler-Interface zugreifen.


## Eine Erweiterung anlegen

Um eine neue Erweiterung anzulegen, folgen Sie dem Link "Erweiterungen
verwalten" und klicken Sie auf die Schaltfläche "Erweiterung hinzufügen". Sie
gelangen nun zu einem Formular, in das Sie die Daten der Erweiterung eingeben
können. Der Kasten oberhalb des Formulars enthält wichtige Hinweise zur
Namensgebung, die Sie unbedingt berücksichtigen sollten.

![](https://raw.github.com/contao/docs/3.0/manual/de/images/erweiterung-hinzufuegen.jpg)

Folgende Kategorien sind momentan verfügbar:

<table>
<tr>
  <th>Kategorie</th>
  <th>Beschreibung</th>
</tr>
<tr>
  <td>Anwendung</td>
  <td>Die Erweiterung ist eine eigenständige Anwendung.</td>
</tr>
<tr>
  <td>Hilfsprogramm</td>
  <td>Die Erweiterung ist ein Hilfsprogramm für das Backend.</td>
</tr>
<tr>
  <td>Vorlage</td>
  <td>Die Erweiterung ist ein Template.</td>
</tr>
<tr>
  <td>Widget</td>
  <td>Die Erweiterung ist ein Eingabefeld (Widget) für Formulare.</td>
</tr>
<tr>
  <td>Plugin</td>
  <td>Die Erweiterung ist eine PHP- oder JavaScript-Library.</td>
</tr>
<tr>
  <td>Andere</td>
  <td>Die Erweiterung passt in keine der genannten Kategorien.</td>
</tr>
</table>


## Eine Freigabe hinzufügen

Nachdem Sie die Erweiterung angelegt haben, können Sie ein erstes Release
hinzufügen, das im Extension Repository als "Freigabe" bezeichnet wird. Jede
weitere Version der Erweiterung wird später als eigene Freigabe gespeichert.
Wechseln Sie mit Hilfe des entsprechenden Navigationssymbols in die
Freigabenverwaltung und klicken Sie auf die Schaltfläche "Freigabe
hinzufügen".

![](https://raw.github.com/contao/docs/3.0/manual/de/images/freigabe-hinzufuegen.jpg)

Versionsnummern im Extension Repository bestehen immer aus drei Zahlenblöcken,
die die Major-, Minor- und Maintenance-Version kennzeichnen (z.B. "1.0.0"),
sowie einer Angabe zum Entwicklungsstatus (z.B. "beta1"):

<table>
<tr>
  <th>Status</th>
  <th>Beschreibung</th>
</tr>
<tr>
  <td>alpha1 - alpha3</td>
  <td>Es handelt sich um eine Alpha-Version.</td>
</tr>
<tr>
  <td>beta1 - beta3</td>
  <td>Es handelt sich um eine Beta-Version.</td>
</tr>
<tr>
  <td>rc1 - rc3</td>
  <td>Es handelt sich um ein Release Candidate.</td>
</tr>
<tr>
  <td>stable</td>
  <td>Es handelt sich um ein stabiles Release für den produktiven Einsatz.</td>
</tr>
</table>


## Die Dateien hochladen

Als Nächstes müssen Sie dem neuen Release Dateien hinzufügen. Wechseln Sie
dazu in die Dateiverwaltung und klicken Sie dort auf die Schaltfläche "Dateien
hinzufügen/aktualisieren". Sie können nun einzelne Dateien oder ganze
Zip-Archive auf den Server übertragen. Achten Sie dabei darauf, das richtige
Zielverzeichnis auszuwählen, damit die Pfade nach dem Upload stimmen.

![](https://raw.github.com/contao/docs/3.0/manual/de/images/dateien-hinzufuegen.jpg)

![](https://raw.github.com/contao/docs/3.0/manual/de/images/dateien-bearbeiten.jpg)


## Eine Übersetzung hinzufügen

Bevor Sie eine Erweiterung veröffentlichen können, muss mindestens eine
Übersetzung angelegt worden sein. Wechseln Sie in die Sprachverwaltung und
klicken Sie dort auf die Schaltfläche "Sprache hinzufügen". Es empfiehlt sich,
immer auch eine englische Übersetzung anzulegen, da die Benutzer im Backend
grundsätzlich nur die Erweiterungen sehen, die in ihrer jeweiligen Sprache oder
in Englisch verfügbar sind.

![](https://raw.github.com/contao/docs/3.0/manual/de/images/uebersetzung-hinzufuegen.jpg)

![](https://raw.github.com/contao/docs/3.0/manual/de/images/uebersetzung-bearbeiten.jpg)

Fertige Übersetzungen können Sie mit einem Klick auf das entsprechende
Navigationssymbol veröffentlichen.


## Abhängigkeiten speichern

Unter Umständen nutzen Sie in einer Ihrer Erweiterungen die Funktionalität
einer anderen wie z.B. Cronjobs. Für den Betrieb Ihrer Erweiterung ist es also
zwingend notwendig, dass auch die Cron-Erweiterung installiert ist, was im
allgemeinen Sprachgebrauch als "Abhängigkeit" bezeichnet wird. Diese
Abhängigkeiten können im Extension Repository gespeichert werden, so dass bei
der Installation einer Erweiterung automatisch alle für deren Betrieb
benötigten Module ebenfalls installiert werden.

![](https://raw.github.com/contao/docs/3.0/manual/de/images/abhaengigkeit-hinzufuegen.jpg)

Wählen Sie als Erstes die Erweiterung aus, die Sie als Abhängigkeit
hinzufügen möchten, und bestätigen Sie Ihre Auswahl mit "Weiter". Im
nächsten Schritt können Sie die Versionen festlegen, die für den
reibungslosen Betrieb mindestens und höchstens erforderlich sind.


## Die Erweiterung veröffentlichen

Nachdem Sie mindestens eine Freigabe angelegt und mit Dateien befüllt sowie
mindestens eine Übersetzung veröffentlicht und ggf. Abhängigkeiten hinterlegt
haben, können Sie die Erweiterung mit Hilfe des entsprechenden
Navigationssymbols veröffentlichen. Beachten Sie dabei, dass Sie eine
veröffentlichte Erweiterung nicht wieder entfernen können. Um zu prüfen, ob
alles korrekt funktioniert, melden Sie sich im Backend an und führen Sie eine
Testinstallation in der Erweiterungsverwaltung durch.


[1]: https://contao.org/de/register.html
[2]: https://contao.org/de/extension-list.html
