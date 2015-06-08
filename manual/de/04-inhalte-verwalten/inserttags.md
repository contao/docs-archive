## Inserttags

Inserttags sind Platzhalter, die bei der Ausgabe einer Seite durch bestimmte
Inhalte ersetzt werden. So kann beispielsweise das aktuelle Datum angezeigt oder
ein Benutzer mit seinem Namen angesprochen werden. Inserttags können fast
überall in Contao verwendet werden.


### Link-Elemente

Mit den folgenden Inserttags können Seiten und Artikel anhand ihrer ID oder
ihres Alias verlinkt werden.

{% raw %}
<table>
<tr>
  <th>Insert-Tag</th>
  <th>Beschreibung</th>
</tr>
<tr>
  <td><code>{{link::*}}</code></td>
  <td>Dieses Tag wird mit einem Link zu einer internen Seite ersetzt (ersetzen
      Sie * mit der ID oder dem Alias).</td>
</tr>
<tr>
  <td><code>{{link::back}}</code></td>
  <td>Dieses Tag wird mit einem Link zur der zuletzt besuchte Seite ersetzt. Kann auch als
      <code>{{link_open::back}}</code>, <code>{{link_url::back}}</code> und
      <code>{{link_title::back}}</code> verwendet werden.
  </td>
</tr>
<tr>
  <td><code>{{link::login}}</code></td>
  <td>Dieses Tag wird mit einem Link zur Anmeldeseite des aktuellen
      Frontend-Benutzers (falls vorhanden) ersetzt.</td>
</tr>
<tr>
  <td><code>{{link_open::*}}</code></td>
  <td>Wird mit dem öffnenden Tag eines Links zu einer internen Seite ersetzt:
      <code>{{link_open::12}}Hier klicken{{link_close}}</code>.</td>
</tr>
<tr>
  <td><code>{{link_url::*}}</code></td>
  <td>Dieses Tag wird mit der URL einer internen Seite ersetzt: <code>&lt;a
      href="{{link_url::12}}"&gt;Hier klicken&lt;/a&gt;</code>.</td>
</tr>
<tr>
  <td><code>{{link_title::*}}</code></td>
  <td>Dieses Tag wird mit dem Titel einer internen Seite ersetzt: <code>&lt;a
      title="{{link_title::12}}"&gt;Hier klicken&lt;/a&gt;</code>.</td>
</tr>
<tr>
  <td><code>{{link_name::*}}</code></td>
  <td>Dieses Tag wird mit dem Namen einer internen Seite ersetzt: 
      <code>&lt;a&gt;{{link_name::12}}&lt;/a&gt;</code>.</td>
</tr>
<tr>
  <td><code>{{link_close}}</code></td>
  <td>Wird mit dem schließenden Tag eines Links zu einer internen Seite
      ersetzt: <code>{{link_open::12}}Hier klicken{{link_close}}</code>.</td>
</tr>
<tr>
  <td><code>{{article::*}}</code></td>
  <td>Dieses Tag wird mit einem Link zu einem Artikel ersetzt (ersetzen Sie *
      mit der ID oder dem Alias).</td>
</tr>
<tr>
  <td><code>{{article_open::*}}</code></td>
  <td>Wird mit dem öffnenden Tag eines Links zu einem Artikel ersetzt:
      <code>{{article_open::12}}Hier klicken{{link_close}}</code>.</td>
</tr>
<tr>
  <td><code>{{article_url::*}}</code></td>
  <td>Dieses Tag wird mit der URL eines Artikels ersetzt: <code>&lt;a
      href="{{article_url::12}}"&gt;Hier klicken&lt;/a&gt;</code>.</td>
</tr>
<tr>
  <td><code>{{article_title::*}}</code></td>
  <td>Dieses Tag wird mit dem Titel eines Artikels ersetzt: <code>&lt;a
      title="{{article_title::12}}"&gt;Hier klicken&lt;/a&gt;</code>.</td>
</tr>
<tr>
  <td><code>{{news::*}}</code></td>
  <td>Dieses Tag wird mit einem Link zu einer Nachricht ersetzt (ersetzen Sie *
      mit der ID oder dem Alias).</td>
</tr>
<tr>
  <td><code>{{news_open::*}}</code></td>
  <td>Wird mit dem öffnenden Tag eines Links zu einer Nachricht ersetzt:
      <code>{{news_open::12}}Hier klicken{{link_close}}</code>.</td>
</tr>
<tr>
  <td><code>{{news_url::*}}</code></td>
  <td>Dieses Tag wird mit der URL einer Nachricht ersetzt: <code>&lt;a
      href="{{news_url::12}}"&gt;Hier klicken&lt;/a&gt;</code>.</td>
</tr>
<tr>
  <td><code>{{news_title::*}}</code></td>
  <td>Dieses Tag wird mit dem Titel einer Nachricht ersetzt: <code>&lt;a
      title="{{news_title::12}}"&gt;Hier klicken&lt;/a&gt;</code>.</td>
</tr>
<tr>
  <td><code>{{news_feed::*}}</code></td>
  <td>Dieser Tag wird mit der URL zu einem News-Feed ersetzen (ersetzen Sie * mit
      der ID).</td>
</tr>
<tr>
  <td><code>{{event::*}}</code></td>
  <td>Dieses Tag wird mit einem Link zu einem Event ersetzt (ersetzen Sie * mit
      der ID oder dem Alias).</td>
</tr>
<tr>
  <td><code>{{event_open::*}}</code></td>
  <td>Wird mit dem öffnenden Tag eines Links zu einem Event ersetzt:
      <code>{{event_open::12}}Hier klicken{{link_close}}</code>.</td>
</tr>
<tr>
  <td><code>{{event_url::*}}</code></td>
  <td>Dieses Tag wird mit der URL eines Events ersetzt: <code>&lt;a
      href="{{event_url::12}}"&gt;Hier klicken&lt;/a&gt;</code>.</td>
</tr>
<tr>
  <td><code>{{event_title::*}}</code></td>
  <td>Dieses Tag wird mit dem Titel eines Events ersetzt: <code>&lt;a
      title="{{event_title::12}}"&gt;Hier klicken&lt;/a&gt;</code>.</td>
</tr>
<tr>
  <td><code>{{calendar_feed::*}}</code></td>
  <td>Dieser Tag wird mit der URL zu einem Kalender-Feed ersetzen (ersetzen Sie * mit
      der ID).</td>
</tr>
<tr>
  <td><code>{{faq::*}}</code></td>
  <td>Dieses Tag wird mit einem Link zu einer häufig gestellten Frage ersetzt
      (ersetzen Sie * mit der ID oder dem Alias).</td>
</tr>
<tr>
  <td><code>{{faq_open::*}}</code></td>
  <td>Wird mit dem öffnenden Tag eines Links zu einer Frage ersetzt:
      <code>{{faq_open::12}}Hier klicken{{link_close}}</code>.</td>
</tr>
<tr>
  <td><code>{{faq_url::*}}</code></td>
  <td>Dieses Tag wird mit der URL einer Frage ersetzt: <code>&lt;a
      href="{{faq_url::12}}"&gt;Hier klicken&lt;/a&gt;</code>.</td>
</tr>
<tr>
  <td><code>{{faq_title::*}}</code></td>
  <td>Dieses Tag wird mit dem Titel einer Frage ersetzt: <code>&lt;a
      title="{{faq_title::12}}"&gt;Hier klicken&lt;/a&gt;</code>.</td>
</tr>
</table>
{% endraw %}


### Benutzereigenschaften

Mit den folgenden Inserttags können Eigenschaften des angemeldeten Benutzers
ausgebeben werden.

{% raw %}
<table>
<tr>
  <th>Insert-Tag</th>
  <th>Beschreibung</th>
</tr>
<tr>
  <td><code>{{user::firstname}}</code></td>
  <td>Dieses Tag wird mit dem Vornamen des angemeldeten Benutzers ersetzt.</td>
</tr>
<tr>
  <td><code>{{user::lastname}}</code></td>
  <td>Dieses Tag wird mit dem Nachnamen des angemeldeten Benutzers ersetzt.</td>
</tr>
<tr>
  <td><code>{{user::company}}</code></td>
  <td>Dieses Tag wird mit dem Firmennamen des angemeldeten Benutzers
      ersetzt.</td>
</tr>
<tr>
  <td><code>{{user::phone}}</code></td>
  <td>Dieses Tag wird mit der Telefonnummer des angemeldeten Benutzers
      ersetzt.</td>
</tr>
<tr>
  <td><code>{{user::mobile}}</code></td>
  <td>Dieses Tag wird mit der Handynummer des angemeldeten Benutzers
      ersetzt.</td>
</tr>
<tr>
  <td><code>{{user::fax}}</code></td>
  <td>Dieses Tag wird mit der Faxnummer des angemeldeten Benutzers ersetzt.</td>
</tr>
<tr>
  <td><code>{{user::email}}</code></td>
  <td>Dieses Tag wird mit der E-Mail-Adresse des angemeldeten Benutzers
      ersetzt.</td>
</tr>
<tr>
  <td><code>{{user::website}}</code></td>
  <td>Dieses Tag wird mit der Internetadresse des angemeldeten Benutzers
      ersetzt.</td>
</tr>
<tr>
  <td><code>{{user::street}}</code></td>
  <td>Dieses Tag wird mit dem Staßennamen des angemeldeten Benutzers
      ersetzt.</td>
</tr>
<tr>
  <td><code>{{user::postal}}</code></td>
  <td>Dieses Tag wird mit der Postleitzahl des angemeldeten Benutzers
      ersetzt.</td>
</tr>
<tr>
  <td><code>{{user::city}}</code></td>
  <td>Dieses Tag wird mit der Stadt des angemeldeten Benutzers ersetzt.</td>
</tr>
<tr>
  <td><code>{{user::country}}</code></td>
  <td>Dieses Tag wird mit dem Land des angemeldeten Benutzers ersetzt.</td>
</tr>
<tr>
  <td><code>{{user::username}}</code></td>
  <td>Dieses Tag wird mit dem Benutzernamen des angemeldeten Benutzers
      ersetzt.</td>
</tr>
</table>
{% endraw %}


### Seiteneigenschaften

Mit den folgenden Inserttags können Seiteneigenschaften wie z.B. der Seitenname
ausgegeben werden.

{% raw %}
<table>
<tr>
  <th>Insert-Tag</th>
  <th>Beschreibung</th>
</tr>
<tr>
  <td><code>{{page::id}}</code></td>
  <td>Dieses Tag wird mit der ID der aktuellen Seite ersetzt.</td>
</tr>
<tr>
  <td><code>{{page::alias}}</code></td>
  <td>Dieses Tag wird mit dem Alias der aktuellen Seite ersetzt.</td>
</tr>
<tr>
  <td><code>{{page::title}}</code></td>
  <td>Dieses Tag wird mit dem Namen der aktuellen Seite ersetzt.</td>
</tr>
<tr>
  <td><code>{{page::pageTitle}}</code></td>
  <td>Dieses Tag wird mit dem Titel der aktuellen Seite ersetzt.</td>
</tr>
<tr>
  <td><code>{{page::language}}</code></td>
  <td>Dieses Tag wird mit der Sprache der aktuellen Seite ersetzt.</td>
</tr>
<tr>
  <td><code>{{page::parentAlias}}</code></td>
  <td>Dieses Tag wird mit dem Alias der übergeordneten Seite ersetzt.</td>
</tr>
<tr>
  <td><code>{{page::parentTitle}}</code></td>
  <td>Dieses Tag wird mit dem Namen der übergeordneten Seite ersetzt.</td>
</tr>
<tr>
  <td><code>{{page::parentPageTitle}}</code></td>
  <td>Dieses Tag wird mit dem Titel der übergeordneten Seite ersetzt.</td>
</tr>
<tr>
  <td><code>{{page::mainAlias}}</code></td>
  <td>Dieses Tag wird mit dem Alias der übergeordneten Hauptseite ersetzt.</td>
</tr>
<tr>
  <td><code>{{page::mainTitle}}</code></td>
  <td>Dieses Tag wird mit dem Namen der übergeordneten Hauptseite ersetzt.</td>
</tr>
<tr>
  <td><code>{{page::mainPageTitle}}</code></td>
  <td>Dieses Tag wird mit dem Titel der übergeordneten Hauptseite ersetzt.</td>
</tr>
<tr>
  <td><code>{{page::rootTitle}}</code></td>
  <td>Dieses Tag wird mit dem Namen der Webseite ersetzt.</td>
</tr>
<tr>
  <td><code>{{page::rootPageTitle}}</code></td>
  <td>Dieses Tag wird mit dem Titel der Webseite ersetzt.</td>
</tr>
</table>
{% endraw %}


### Umgebungsvariablen

Mit den folgenden Inserttags können Umgebungsvariablen wie z.B. der Seitenname
oder der Request-String ausgegeben werden.

{% raw %}
<table>
<tr>
  <th>Insert-Tag</th>
  <th>Beschreibung</th>
</tr>
<tr>
  <td><code>{{env::host}}</code></td>
  <td>Dieses Tag wird mit dem aktuellen Hostnamen ersetzt.</td>
</tr>
<tr>
  <td><code>{{env::url}}</code></td>
  <td>Dieses Tag wird mit dem Hostnamen und dem Protokoll ersetzt.</td>
</tr>
<tr>
  <td><code>{{env::path}}</code></td>
  <td>Dieses Tag wird mit der aktuellen Basis-URL samt Pfad zum
      Contao-Verzeichnis ersetzt.</td>
</tr>
<tr>
  <td><code>{{env::request}}</code></td>
  <td>Dieses Tag wird mit dem aktuellen Request-String ersetzt.</td>
</tr>
<tr>
  <td><code>{{env::ip}}</code></td>
  <td>Dieses Tag wird mit der IP-Adresse des aktuellen Besuchers ersetzt.</td>
</tr>
<tr>
  <td><code>{{env::referer}}</code></td>
  <td>Dieses Tag wird mit der URL der zuletzt besuchten Seite ersetzt.</td>
</tr>
<tr>
  <td><code>{{env::files_url}}</code></td>
  <td>Dieses Tag wird mit der statischen URL des Uploadverzeichnis ersetzt.</td>
</tr>
<tr>
  <td><code>{{env::assets_url}}</code></td>
  <td>Dieses Tag wird mit der statischen URL des Assets-Verzeichnis ersetzt.</td>
</tr>
</table>
{% endraw %}


### Include-Elemente

Mit den folgenden Inserttags können Ressourcen wie z.B. Artikel, Module oder
Dateien aus dem "templates"-Verzeichnis eingebunden werden.

{% raw %}
<table>
<tr>
  <th>Insert-Tag</th>
  <th>Beschreibung</th>
</tr>
<tr>
  <td><code>{{insert_article::*}}</code></td>
  <td>Dieses Tag wird mit dem referenzierten Artikel ersetzt (ersetzen Sie * mit
      der ID oder dem Alias).</td>
</tr>
<tr>
  <td><code>{{insert_content::*}}</code></td>
  <td>Dieses Tag wird mit dem referenzierten Inhaltselement ersetzt (ersetzen
      Sie * mit der ID des Elements).</td>
</tr>
<tr>
  <td><code>{{insert_module::*}}</code></td>
  <td>Dieses Tag wird mit dem referenzierten Modul ersetzt (ersetzen Sie * mit
      der ID des Moduls).</td>
</tr>
<tr>
  <td><code>{{insert_form::*}}</code></td>
  <td>Dieses Tag wird mit dem referenzierten Formular ersetzt (ersetzen Sie * mit
      der ID des Formulars).</td>
</tr>
<tr>
  <td><code>{{article_teaser::*}}</code></td>
  <td>Dieses Tag wird mit dem Teaser eines Artikels ersetzt (ersetzen Sie * mit
      der ID des Artikels).</td>
</tr>
<tr>
  <td><code>{{news_teaser::*}}</code></td>
  <td>Dieses Tag wird mit dem Teaser einer Nachricht ersetzt (ersetzen Sie * mit
      der ID der Nachricht).</td>
</tr>
<tr>
  <td><code>{{event_teaser::*}}</code></td>
  <td>Dieses Tag wird mit dem Teaser eines Events ersetzt (ersetzen Sie * mit
      der ID des Events).</td>
</tr>
<tr>
  <td><code>{{file::*}}</code></td>
  <td>Dieses Tag wird mit dem Inhalt einer .php-, .tpl-, .xhtml- oder 
      .html5-Datei aus dem "templates"-Verzeichnis ersetzt (ersetzen Sie * mit
      dem Namen). Bei Bedarf können Sie Argumente übergeben: 
      <code>{{file::file.php?arg1=val}}</code>.
      Mittels UUID kann außerdem der Pfad einer Datei aus der Datenbank 
      abgefragt werden:
      <code>{{file::6939a448-9b30-11e4-bcba-079af1e9baea}}</code>.</td>
</tr>
</table>
{% endraw %}


### Verschiedenes

Mit den folgenden Inserttags können Sie verschiedene Aufgaben erledigen und
z.B. das aktuelle Datum oder ein Lightbox-Bild einfügen.

{% raw %}
<table>
<tr>
  <th>Insert-Tag</th>
  <th>Beschreibung</th>
</tr>
<tr>
  <td><code>{{date}}</code></td>
  <td>Dieses Tag wird mit dem aktuellen Datum gemäß des globalen Datumsformats
      ersetzt.</td>
</tr>
<tr>
  <td><code>{{date::*}}</code></td>
  <td>Dieses Tag wird mit dem aktuellen Datum gemäß eines individuellen
      Datumsformats ersetzt.</td>
</tr>
<tr>
  <td><code>{{last_update}}</code></td>
  <td>Dieses Tag wird mit dem Datum der letzten Aktualisierung gemäß des
      globalen Datumsformats ersetzt.</td>
</tr>
<tr>
  <td><code>{{last_update::*}}</code></td>
  <td>Dieses Tag wird mit Datum der letzten Aktualisierung gemäß eines
      individuellen Datumsformats ersetzt.</td>
</tr>
<tr>
  <td><code>{{email::*}}</code></td>
  <td>Dieses Tag wird mit einem verschlüsselten Link zu einer E-Mail-Adresse
      ersetzt.</td>
</tr>
<tr>
  <td><code>{{email_open::*}}</code></td>
  <td>Dieses Tag wird mit einem verschlüsselten Link zu einer E-Mail-Adresse
      ersetzt. Allerdings wird das schließende <code>&lt;/a&gt;</code> nicht
      angefügt.</td>
</tr>
<tr>
  <td><code>{{email_url::*}}</code></td>
  <td>Dieses Tag wird nur durch die verschlüsselte E-Mail-Adresse ersetzt.</td>
</tr>
<tr>
  <td><code>{{lang::*}}</code></td>
  <td>Mit diesem Tag können fremdsprachige Wörter in einem Text markiert
      werden: <code>{{lang::fr}}Au revoir{{lang}}</code>. Dies wird ersetzt mit
      <code>&lt;span lang="fr"&gt;Au revoir&lt;/span&gt;</code> und fügt
      <code>xml:lang="fr"</code> hinzu falls das Seitenformat XHTML ist.
  </td>
</tr>
<tr>
  <td><code>{{abbr::*}}</code></td>
  <td>Abkürzungen in einem Text markieren: <code>{{abbr::World Wide
      Web}}WWW{{abbr}}</code>. Dies wird ersetzt mit <code>&lt;abbr title="World
      Wide Web"&gt;WWW&lt;/abbr&gt;</code>.</td>
</tr>
<tr>
  <td><code>{{acronym::*}}</code></td>
  <td>Akronyme in einem Text markieren: <code>{{acronym::Multipurpose Internet
      Mail Extensions}}MIME{{acronym}}</code>. Dies wird ersetzt mit <code>&lt;acronym
      title="Multipurpose Internet Mail Extensions"&gt;MIME&lt;/acronym&gt;</code>.</td>
</tr>
<tr>
  <td><code>{{ua::*}}</code></td>
  <td>Eigenschaften des Browsers (User Agent) ausgeben: <code>{{ua::browser}}</code>.
      Dies wird beispielsweise ersetzt mit "chrome".</td>
</tr>
<tr>
  <td><code>{{iflng::*}}</code></td>
  <td>Dieses Tag wird komplett entfernt, wenn die Sprache der Seite nicht mit
      der Tag-Sprache übereinstimmt. Sie können so sprachspezifische Bezeichnungen
      erstellen: <code>{{iflng::en}}Your name{{iflng::de}}Ihr Name{{iflng}}</code></td>
</tr>
<tr>
  <td><code>{{ifnlng::*}}</code></td>
  <td>Dieses Tag wird komplett entfernt, wenn die Sprache der Seite mit der
      Tag-Sprache übereinstimmt. Sie können so sprachspezifische Bezeichnungen
      erstellen: <code>{{ifnlng::de}}Your name{{ifnlng}}{{iflng::de}}Ihr Name{{iflng}}</code></td>
</tr>
<tr>
  <td><code>{{image::*}}</code></td>
  <td>Dieses Tag wird mit der Vorschauansicht eines Bildes ersetzt (wobei *
  eine Datenbank ID, eine UUID oder ein Pfad aus dem Dateisystem sein kann):
<code>{{image::58ca4a90-2d30-11e4-8c21-0800200c9a66?width=200&amp;height=150}}</code>.<br>
      <strong>width</strong>: Breite des Vorschaubildes,<br>
      <strong>height</strong>: Höhe des Vorschaubildes,<br>
      <strong>alt</strong>: Alternativer Text,<br>
      <strong>class</strong>: CSS-Klasse,<br>
      <strong>rel</strong>: rel-Attribut (z.B. "lightbox"),<br>
      <strong>mode</strong>: Modus ("proportional", "crop" oder "box").</td>
</tr>
<tr>
  <td><code>{{label::*}}</code></td>
  <td>Dieses Tag wird mit einer Übersetzung ersetzt. Der erste Parameter ist
      der Name einer Sprachdatei oder einem Akronym (z.B. <code>CNT</code> für
      Länder oder <code>LNG</code> für Sprachen). Beispiele:
      <code>{{label::CNT:au}}</code> wird zu "Australien" und 
      <code>{{label::tl_article:title:0}}</code> wird zu "Titel". 
      Beachten Sie, dass innerhalb des Pfads zur Bezeichnung nur einfache
      Doppelpunkte verwendet werden.</td>
</tr>
<tr>
  <td><code>{{version}}</code></td>
  <td>Dieses Tag wird mit der verwendeten Contao-Version (z.B. 3.2.7)
      ersetzt.</td>
</tr>
<tr>
  <td><code>{{request_token}}</code></td>
  <td>Dieses Tag wird mit dem zur aktuellen Session gehörenden Request-Token
      ersetzt.</td>
</tr>
<tr>
  <td><code>{{toggle_view}}</code></td>
  <td>Dieses Tag wird mit einem Link ersetzt, welcher zwischen Mobile- und
      Desktop-Layout wechselt.</td>
</tr>
<tr>
  <td><code>{{br}}</code></td>
  <td>Dieses Tag wird mit einem HTML <code>&lt;br&gt;</code> Element
  (Zeilenumbruch) ersetzt.</td>
</tr>
</table>
{% endraw %}


### Inserttag-Flags

Mittels Flags können Sie Insert-Tags weiter verarbeiten. Der Wert kann damit
z.B. einer PHP-Funktion übergeben werden. Beliebig viele Flags können
miteinander kombiniert werden:

{% raw %}
```
{{ua::browser|uncached}}
{{page::title|decodeEntities|strtoupper}}
```
{% endraw %}

Verfügbare Flags:

<table>
<tr>
    <th>Flag</th>
    <th>Beschreibung</th>
    <th>Weitere Informationen</th>
</tr>
<tr>
    <td><code>uncached</code></td>
    <td>Erhält das Tag beim Schreiben der Cache-Datei.</td>
    <td></td>
</tr>
<tr>
    <td><code>refresh</code></td>
    <td>Erstellt die Ausgabe bei jeder Anfrage neu.</td>
    <td></td>
</tr>
<tr>
    <td><code>addslashes</code></td>
    <td>Stellt bestimmten Zeichen eines Strings ein "\" voran.</td>
    <td><a target="_blank" href="http://php.net/addslashes">PHP-Funktion</a></td>
</tr>
<tr>
    <td><code>stripslashes</code></td>
    <td>Entfernt das "\" vor bestimmten Zeichen eines Strings.</td>
    <td><a target="_blank" href="http://php.net/stripslashes">PHP-Funktion</a></td>
</tr>
<tr>
    <td><code>standardize</code></td>
    <td>Standardisiert die Ausgabe (z.B. das Alias bei der Seitenstruktur).</td>
    <td></td>
</tr>
<tr>
    <td><code>ampersand</code></td>
    <td>Wandelt Und-Zeichen in Entities um.</td>
    <td></td>
</tr>
<tr>
    <td><code>specialchars</code></td>
    <td>Wandelt Sonderzeichen in Entities um.</td>
    <td></td>
</tr>
<tr>
    <td><code>nl2br</code></td>
    <td>Fügt vor allen Zeilenumbrüchen eines Strings HTML-Zeilenumbrüche ein.</td>
    <td><a target="_blank" href="http://php.net/nl2br">PHP-Funktion</a></td>
</tr>
<tr>
    <td><code>nl2br_pre</code></td>
    <td>Erhält die Zeilenumbrüche innerhalb von <code>&lt;pre&gt;</code>-Tags.</td>
    <td></td>
</tr>
<tr>
    <td><code>strtolower</code></td>
    <td>Wandelt die Ausgabe in Kleinbuchstaben um.</td>
    <td><a target="_blank" href="http://php.net/strtolower">PHP-Funktion</a></td>
</tr>
<tr>
    <td><code>utf8_strtolower</code></td>
    <td>Unicode-bewusste Umwandlung in Kleinbuchstaben</td>
    <td></td>
</tr>
<tr>
    <td><code>strtoupper</code></td>
    <td>Wandelt die Ausgabe in Großbuchstaben um.</td>
    <td><a target="_blank" href="http://php.net/strtoupper">PHP-Funktion</a></td>
</tr>
<tr>
    <td><code>utf8_strtoupper</code></td>
    <td>Unicode-bewusste Umwandlung in Großbuchstaben</td>
    <td></td>
</tr>
<tr>
    <td><code>ucfirst</code></td>
    <td>Wandelt das erste Zeichen in einen Großbuchstaben um.</td>
    <td><a target="_blank" href="http://php.net/ucfirst">PHP-Funktion</a></td>
</tr>
<tr>
    <td><code>lcfirst</code></td>
    <td>Wandelt das erste Zeichen in einen Kleinbuchstaben um.</td>
    <td><a target="_blank" href="http://php.net/lcfirst">PHP-Funktion</a></td>
</tr>
<tr>
    <td><code>ucwords</code></td>
    <td>Wandelt das erste Zeichen jedes Wortes in einen Großbuchstaben um.</td>
    <td><a target="_blank" href="http://php.net/ucwords">PHP-Funktion</a></td>
</tr>
<tr>
    <td><code>trim</code></td>
    <td>Entfernt Leerzeichen vom Anfang und Ende der Ausgabe.</td>
    <td><a target="_blank" href="http://php.net/trim">PHP-Funktion</a></td>
</tr>
<tr>
    <td><code>rtrim</code></td>
    <td>Entfernt Leerzeichen vom Anfang der Ausgabe.</td>
    <td><a target="_blank" href="http://php.net/rtrim">PHP-Funktion</a></td>
</tr>
<tr>
    <td><code>ltrim</code></td>
    <td>Entfernt Leerzeichen vom Ende der Ausgabe.</td>
    <td><a target="_blank" href="http://php.net/ltrim">PHP-Funktion</a></td>
</tr>
<tr>
    <td><code>utf8_romanize</code></td>
    <td>Romanisiert die Ausgabe.</td>
    <td></td>
</tr>
<tr>
    <td><code>strrev</code></td>
    <td>Dreht die Ausgabe um.</td>
    <td><a target="_blank" href="http://php.net/strrev">PHP-Funktion</a></td>
</tr>
<tr>
    <td><code>encodeEmail</code></td>
    <td>Kodiert E-Mail-Adressen in der Ausgabe.</td>
    <td>siehe <code>String::encodeEmail</code></td>
</tr>
<tr>
    <td><code>decodeEntities</code></td>
    <td>Dekodiert Entities in der Ausgabe.</td>
    <td>siehe <code>String::decodeEntities()</code></td>
</tr>
<tr>
    <td><code>number_format</code></td>
    <td>Formatiert eine Zahl (keine Dezimalstellen).</td>
    <td>siehe <code>System::getFormattedNumber()</code></td>
</tr>
<tr>
    <td><code>currency_format</code></td>
    <td>Formatiert eine Währung (zwei Dezimalstellen).</td>
    <td>siehe <code>System::getFormattedNumber()</code></td>
</tr>
<tr>
    <td><code>readable_size</code></td>
    <td>Wandelt die Ausgabe in ein menschenlesbares Format um.</td>
    <td>siehe <code>System::getReadableSize()</code></td>
</tr>
<tr>
    <td><code>urlencode</code></td>
    <td>URL-kodiert einen String.</td>
    <td><a target="_blank" 
    href="http://php.net/urlencode">PHP-Funktion</a></td>
</tr>
<tr>
    <td><code>rawurlencode</code></td>
    <td>URL-Kodierung nach RFC 3986.</td>
    <td><a target="_blank" 
    href="http://php.net/rawurlencode">PHP-Funktion</a></td>
</tr>
</table>
