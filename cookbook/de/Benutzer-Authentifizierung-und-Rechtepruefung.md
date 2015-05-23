# Benutzer-Authentifizierung und Rechteprüfung

Nachfolgend wird beschrieben, wie man den Authentifizierungstatus und die
Rechte eines Benutzers in einer eigenen Erweiterung prüfen kann.


## Backend

Grundsätzlich nimmt Contao die Benutzerauthentifizierung automatisch vor. Der
Code für das Backend befindet sich in der Datei `contao/main.php`:

```php
public function __construct()
{
    $this->import('BackendUser', 'User');
    parent::__construct();

    $this->User->authenticate();
}
```


### Aufruf des Benutzer-Objektes im Backend

Das Benutzer-Objekt lässt sich in der eigenen Erweiterung auf zwei Arten
aufrufen:

```php
$objUser = BackendUser::getInstance();
echo $objUser->username;

// Im Objekt-Kontext
$this->import('BackendUser', 'User');
echo $this->User->username;
```

Da der Zugang zum Backend grundsätzlich nicht ohne Authentifizierung möglich
ist, kann davon ausgegangen werden, dass es dort immer einen authentifizierten
Benutzer gibt.


### Prüfung des Admin-Status

Einen Administrator erkennt man am `isAdmin`-Flag:

```php
if ($objUser->isAdmin) {
    // alles ist erlaubt
}
```


### Prüfung der Benutzergruppen

Ein normaler Benutzer gehört in der Regel einer oder mehreren Benutzergruppen
an, deren Zugehörigkeit über die Methode `isMemberOf()` geprüft werden kann:


```php
if ($objUser->isMemberOf(3)) {
    // der Benutzer gehört der Gruppe mit der ID 3 an
}
```

Ein Array der IDs aller Benutzergruppen, denen ein Benutzer angehört, lässt sich
über das Feld `groups` abfragen:

```php
print_r($objUser->groups);
```


### Prüfung der Zugriffsrechte

Es gibt zwei Methoden, die hauptsächlich für die Prüfung der Zugriffsrechte
zuständig sind:

 - `hasAccess()`: prüft, ob ein Benutzer ein bestimmtes Recht hat
 - `isAllowed()`: prüft, ob eine bestimmte Aktion auf einer Seite erlaubt ist


#### Die Methode `hasAccess()`

Mit der Methode `hasAccess()` lässt sich beispielsweise prüfen, ob ein Benutzer
Zugriff auf ein Backend-Modul hat:

```php
if ($objUser->hasAccess('news', 'modules')) {
    // der Benutzer darf auf das News-Modul zugreifen
}
```

Es lässt sich auch prüfen, ob der Zugriff auf ein bestimmtes News-Archiv erlaubt
ist:

```php
if ($objUser->hasAccess(2, 'news')) {
    // der Benutzer darf auf das News-Archiv mit der ID 2 zugreifen
}
```

Oder ob der Benutzer das Recht hat, neue News-Feeds anzulegen:

```php
if ($objUser->hasAccess('create', 'newsfeedp')) {
    // der Benutzer hat das Recht, neue News-Feeds anzulegen
}
```

Ebenfalls lassen sich die Page- und Filemounts des Benutzers prüfen:

```php
if ($objUser->hasAccess(11, 'pagemounts')) {
    // der Benutzer darf auf die Seite mit der ID 11 zugreifen
}
```

Schlussendlich lässt sich auch der Zugriff auf jedes einzelne Feld jeder Tabelle
mit der Methode `hasAccess()` prüfen:

```php
if ($objUser->hasAccess('tl_faq::published', 'alexf')) {
    // der Benutzer darf auf das Feld "published" der Tabelle "tl_faq" zugreifen
}
```

Der zweite Parameter der Methode `hasAccess()` bezieht sich auf das Feld in der
Tabelle `tl_user` bzw. `tl_user_group`, in dem die jeweilige Berechtigung
gespeichert ist. Zum Beispiel fragt "modules" das Feld `tl_user.modules` bzw.
`tl_user_group.modules` ab.


#### Die Methode `isAllowed()`

Mit der Methode `isAllowed()` lässt sich prüfen, welche Rechte der Benutzer auf
einer bestimmten Seite hat (Zugriffsrechte).

```php
$objPage = PageModel::findByPk(6);

if ($objUser->isAllowed(1, $objPage->row())) {
    // der Benutzer darf die Seite mit der ID 6 bearbeiten
}

if ($objUser->isAllowed(2, $objPage->row())) {
    // der Benutzer darf die Hierarchie der Seite mit der ID 6 ändern
}

if ($objUser->isAllowed(3, $objPage->row())) {
    // der Benutzer darf die Seite mit der ID 6 löschen
}

if ($objUser->isAllowed(4, $objPage->row())) {
    // der Benutzer darf die Artikel der Seite mit der ID 6 bearbeiten
}

if ($objUser->isAllowed(5, $objPage->row())) {
    // der Benutzer darf die Hierarchie der Artikel der Seite mit der ID 6 ändern
}

if ($objUser->isAllowed(6, $objPage->row())) {
    // der Benutzer darf die Artikel der Seite mit der ID 6 löschen
}
```


## Frontend

Auch im Frontend erfolgt die Authentifizierung automatisch, allerdings kann man
nicht davon ausgehen, dass es immer ein authentifiziertes Mitglied gibt.


### Aufruf des Benutzer-Objektes im Frontend

Das Benutzer-Objekt lässt sich in der eigenen Erweiterung auf zwei Arten
aufrufen:

```php
$objUser = FrontendUser::getInstance();
echo $objUser->username;

// Im Objekt-Kontext
$this->import('FrontendUser', 'User');
echo $this->User->username;
```

Den Login-Status kann man über die Konstante `FE_USER_LOGGED_IN` abfragen:

```php
if (FE_USER_LOGGED_IN === true) {
    $objUser = FrontendUser::getInstance();
    // es gibt einen authentifizierten Frontend-Benutzer
} else {
    // es gibt keinen authentifizierten Frontend-Benutzer
}
```


### Prüfung der Mitgliedergruppen

Im Frontend erfolgt die Zugriffsprüfung auf Basis der Gruppenzugehörigkeit, die
sich über die Methode `isMemberOf()` abrufen lässt:


```php
if ($objUser->isMemberOf(3)) {
    // der Benutzer gehört der Gruppe mit der ID 3 an
}
```

Ein Array der IDs aller Mitgliedergruppen, denen ein Mitglied angehört, lässt
sich über das Feld `groups` abfragen:

```php
print_r($objUser->groups);
```
