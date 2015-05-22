## Internen Cache umgehen

Vor der Anpassung von Contao oder der Entwicklung von Erweiterungen sollte
unbedingt der interne Cache deaktiviert bzw. umgangen werden.
Dazu navigieren Sie im Backend zu "System"->"Einstellungen" und setzten einen
Haken unter "Globale Einstellungen" bei "Internen Cache umgehen".

![](images/internen-cache-umgehen.jpg)

Sobald die Seite jedoch in den produktiven Betrieb geht, sollte unbedingt der
Haken bei "Internen Cache umgehen" entfernt werden, da das System ohne den
Cache gerade bei größeren Projekten um einiges langsamer reagiert.
