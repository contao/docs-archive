## Themes

Obwohl der Theme-Manager eine neue Funktion der Version 2.9 ist, handelt es sich
dabei eigentlich nur um ein erweitertes Interface für etwas, das es in Contao
schon immer gegeben hat. Das Design einer Webseite besteht normalerweise aus
Stylesheets, Frontendmodulen, Seitenlayouts, Dateien und Templates, die Sie im
Contao-Backend verwalten können. Der Theme-Manager ändert diesen Ansatz nicht,
er fügt lediglich eine Möglichkeit hinzu, die Ressourcen zu exportieren und
wieder zu importieren ([Video-Einführung ansehen][1]).


### Themes versus Frontend-Templates

Der Hauptunterschied zwischen [Themes][2] und Frontend-Templates ist, dass ein
Frontend-Template eine vollständig vorkonfigurierte Beispielwebseite mit einer
beispielhaften Seitenstruktur, Artikeln, Inhaltselementen und sogar Benutzern
und Gruppen enthält. Ein Theme enthält dagegen nur das eigentliche Design der
Webseite und kann deswegen importiert werden, ohne dass bestehende Daten
verloren gehen.

![](images/themes-verwalten.jpg?raw=true)


### Theme-Bestandteile

Ein Theme ist eine Gruppe von [Stylesheets][3], [Frontend-Modulen][4] und
[Seitenlayouts][5], die alle in der Datenbank gespeichert sind und automatisch
vom Theme Exporter erkannt werden. Sie werden diese Elemente in den nächsten
Abschnitten näher kennenlernen. Ein Theme beinhaltet darüber hinaus meistens
auch Bilder und andere Dateien aus dem Files-Verzeichnis sowie optional
angepasste Templates aus dem Templates-Verzeichnis. Diese Ressourcen sind jedoch
nicht automatisch mit dem Theme verlinkt und müssen deswegen in den
Theme-Einstellungen hinzugefügt werden, damit sie beim Theme-Export
berücksichtigt werden.

![](images/theme-einstellungen.jpg?raw=true)


### Theme-Export und -Import

Um ein Theme zu exportieren, klicken Sie einfach auf die Export-Schaltfläche
und speichern Sie die .cto-Datei auf Ihrem lokalen Computer. Obwohl .cto eine
proprietäre Dateiendung für Contao-Themes ist, handelt es sich dabei
eigentlich um ZIP-Archive, die Sie mit jedem Programm entpacken können, das
.zip-Dateien unterstützt. Um ein Theme zu reimportieren, übertragen Sie die
.cto-Datei auf Ihren Webserver, öffnen Sie den Theme-Manager im Contao-Backend
und klicken Sie auf "Theme importieren". Sie können mehrere Themes auf einmal
importieren. Nachdem der Import abgeschlossen ist, können Sie das Seitenlayout
des neuen Themes in der Seitenstruktur zuweisen.


[1]: http://www.youtube.com/watch?v=6z744hsR8I0
[2]: https://contao.org/de/contao-themes-and-templates.html
[3]: 03-seiten-verwalten/stylesheets.md#stylesheets
[4]: 03-seiten-verwalten/module.md#module
[5]: 03-seiten-verwalten/seitenlayouts.md#seitenlayouts