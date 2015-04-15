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
