Erweiterung entwicklen
======================

Für das Testen der Erweiterung auf einer lokalen Contao-Installation in den Einstellungen (Backend:
_System_ -> _Einstellungen_) die beiden folgenden Optionen aktivieren:

- _Globale Einstellungen_ -> _Internen Cache umgehen_
- _Sicherheitseinstellungen_ -> _Fehlermeldungen anzeigen_

Den Button _Speichern_ bzw. _Speichern und schließen_ nicht vergessen.

Zur Sicherheit im Anschluss den internen Cache noch mal leeren. Das geht im Backend im Punkt
_System_ -> _Systemwartung_. Auf dieser Seite _Daten bereinigen_ -> _Internen Cache leeren_
auswählen und den den Button _Daten bereinigen_ nicht vergessen.


Best Practices
==============

Namespaces
----------

[Auf Empfehlung vom Contao Team](https://community.contao.org/de/showthread.php?30961-Contao-3-und-Namespace&p=203762&viewfull=1#post203762)
sollten Namespace in Erweiterungen für Contao nicht verwendet werden.

Der Grund dafür ist dass Namespaces in Contao, nicht wie von Programmiersprachen vorgesehen, zur
Unterteilung des globalen Namespaces und zur Paketierung von Softwaremodulen verwendet werden. In
Contao wurden Namespaces nur eingeführt, um die Klassen des Cores ersetzen zu können.

Durch den Verzicht auf Namespaces erspart man sich den Ärger, dass Klassen womöglich nicht korrekt
oder gar nicht geladen werden können.
