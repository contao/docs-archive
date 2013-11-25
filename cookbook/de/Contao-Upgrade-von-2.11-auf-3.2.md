Contao Upgrade von 2.11 auf 3.2
===============================

__Als erstes ein Backup des Dateisystems und der Datenbank von Contao 2.11
machen!!__

Am einfachsten geht das Upgrade, wenn man direkten Zugriff auf den Server hat.
Als Alternative kann man das Upgrade auf einem lokalen Rechner durchführen.
Dabei sollte man in der Zwischenzeit die Webseite im Internet abschalten, weil
Änderungen dort nicht bzw. nur manuell nach dem Zurückspielen der lokalen Kopie
übernommen werden können.

Das Upgrade führe ich auf einer Kopie durch, die ich parallel zu meiner
bestehenden Webseite laufen habe. Die Kopie kann wie im
[Handbuch](https://contao.org/de/manual/3.2/installation.html#eine-installation-umziehen)
beschrieben gemacht werden. Parallel zum 2.11-Original und zur 2.11-Kopie wird
noch ein Contao 3.2 gelegt. Wobei Contao 3.2 nur entpackt und noch nicht
installiert wird. Im Dateisystem sieht das dann wie folgt aus:

```
htdocs/contao-2.11-original
htdocs/contao-2.11-copy
htdocs/contao-3.2
```

Und in der Datenbank gibt es auch zwei Datenbanken:

```
contao_2.11_original
contao_2.11_copy
contao_3.2
```

__Hinweis:__ Den Unterstrich verwende ich im Namen der Datenbank, weil
_phpMyAdmin_ den Unterstrich zum Gruppieren von Datenbanken interpretiert.


Upgrade vorbereiten
-------------------

Die folgenden Schritte werden auf der 2.11-Kopie durchgeführt. Das 2.11-Original
ist nur noch zum Vergleich alt vs. neu da.

Im Backend in der _Erweiterungsverwaltung_ alle installierten Erweiterungen auf
Kompatibilität mit Contao 3.2 prüfen:

- Eine Erweiterung, die mit Contao 2.11 bis 3.x kompatibel ist, aktualisieren.
  Erweiterungen die nur bis 3.0 oder 3.1 kompatibel sind, sollten auch unter 3.2
  funktionieren.
- Eine Erweiterung, die nur bis Contao 2.11 kompatibel ist deinstallieren. Bei
  diesen Erweiterungen ist davon auszugehen, dass sie nicht mehr funktionieren.
  Die Tabellen und Spalten dabei aber nicht entfernen, wenn man die Daten später
  weiterverwenden möchte!! Der Entwickler der Erweiterung kann später eine
  aktualisierte Version veröffentlichen oder man migriert die Daten zu einer
  anderen Erweiterung.
- Eine Erweiterung die nicht mehr mit Contao 2.11, dafür aber nur noch mit
  Contao 3.x kompatibel ist unverändert belassen.

__Achtung:__ Nicht nur die Erweiterungen prüfen, die man selbst installiert hat,
sondern auch die automatisch installierten Abhängigkeiten.

Im Anschluss im Backend in den _Einstellungen_ die Option _Abgesicherter Modus_
aktivieren. Damit werden alle verbleibenden Erweiterungen vorerst deaktiviert.


Upgrade durchführen
-------------------

Im 3.2-Verzeichnis liegt ein entpacktes, nicht installiertes Contao 3.2. Die
3.2-Datenbank ist entsprechend noch leer.

Die folgenden Schritte werden auf der 2.11-Kopie durchgeführt. Das 2.11-Original
ist nur noch zum Vergleich alt vs. neu da.

1. Den Inhalt der 2.11-Datenbank in die 3.2-Datenbank kopieren.
2. Das Verzeichnis `tl_files` in das 3.2-Verzeichnis kopieren.
3. Das Verzeichnis `templates` in das 3.2-Verzeichnis kopieren
4. Die Datei `system/config/dcaconfig.php` in das 3.2-Verzeichnis kopieren
5. Die Datei `system/config/initconfig.php` in das 3.2-Verzeichnis kopieren
6. Die Datei `system/config/langconfig.php` in das 3.2-Verzeichnis kopieren
7. Die Datei `system/config/localconfig.php` in das 3.2-Verzeichnis kopieren
8. In der Datei `system/config/localconfig.php` die Datenbank auf die
   3.2-Datenbank ändern.

Im Anschluss das Installtool aus dem 3.2-Verzeichnis aufrufen.

Wenn alles richtig läuft, fragt das Installtoll nach dem Passwort der alten
2.11-Installation. Die Datenbank wird erkannt und das Installtool fordert auf,
die Datenbank auf 3.0 zu aktualisieren.

Die Datenbankaktualisierung wird in mehreren Schritten durchgeführt, also
solange auf den Button drücken, bis es vorbei ist. Aber Achtung, zwischen den
Klicks immer abwarten, bis der jeweilige Schritt abgeschlossen ist!!

Nach dem Upgrade der Datenbank sind noch einfache Aktualisierung notwendig, hier
nur neue Tabellen und Spalten anlegen. Es sollten keine vorhandenen Tabellen
oder Spalten gelöscht werden!

Damit ist das Upgrade auf Contao 3.2 eigentlich schon erledigt. Nun müssen nur
noch die Erweiterungen wieder zum Laufen gebracht werden.

__Hinweis__: Die Webseite ist jetzt im _Wartungsmodus_, das heißt nur die
Administratoren können die Webseite über das Backend benutzen. Das Frontend ist
gesperrt.

Upgrade nachbereiten
--------------------

Jetzt müssen noch alle vorhandenen Erweiterungen aktualisiert wird.

Da wir die Modul-Verzeichnisse nicht kopiert haben, kommt die
_Erweiterungsverwaltung_ im Backend nicht damit klar, die physisch nicht mehr
vorhanden Erweiterungen zu aktualisieren. Wahrscheinlich versucht sie nur die
geänderten Dateien zu aktualisieren. Diese Optimierung ist im Normalfall
berechtigt, hier stört es ein wenig. Deswegen die Erweiterungen einzeln
anklicken und auf der Beschreibungsseite unten den _Installieren_-Button
verwenden. Hierbei werden alle Dateien erneut installiert. Beim Anschließenden
Datenbankkaktualisieren, merkt der Installer, dass die Tabellen und Spalten
schon da sind. Somit können wir die Daten weiterverwenden.

__Achtung:__ Dieses Vorgehehen funktioniert nur mit Erweiterungen die keine
eigenen Daten speichern oder nur in der Datenbank speichern.

__Hinweis:__ Nicht wundern, wenn die Datenbankaktualisierung Tabellen oder
Spalten ändern will, die schon da sind. Da sich die Verwaltung der Datenbank
von 2.11 zu 3.2 geändert hat, erkennt das Tool die richtige Struktur noch nicht,
wenn einige Erweiterungen noch nicht aktualisiert sind.

Nach dem alle Erweiterungen auf dem neuesten Stand sind, sollten bei der
Datenbankaktualisierung nur noch Tabellen und Spalten aufgeführt werden, die
gelöscht werden können. Diese sollten noch nicht gelöscht, wenn man die Daten
später weiterverwenden möchte, z.B. wenn der Entwickler seine Erweiterung für
Contao 3.2 angepasst hat oder man die Daten zu einer anderen Erweiterung
migrieren möchte.

Zum Schluss muss noch der Wartungsmodus und der absicherten Modus wieder
abgeschalten werden. Das man ganz bequem über die rote Leiste am oberen
Bildschirmrand im Backend erledigen.

Zum Schluss bleibt nur die Entwickler von noch nicht angepassten Erweiterungen
zusammenzuschei..., freundlich zu bitten ihre Erweiterungen anzupassen ;-)

Viel Spaß mit der neuen LTS-Version von Contao.
