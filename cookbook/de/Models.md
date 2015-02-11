# Models

Ein *Model* repräsentiert einen Datensatz aus einer Tabelle (Entität). Models 
bieten einen Objekt-orientierten Zugriff auf Tabellen und ersetzen damit SQL-
Statements  weitgehend. Darüber hinaus bieten sie viele weitere Vorteile.
Mehrere Models werden durch eine *Collection* referenziert, dies entspricht 
einer SQL-Abfrage, die mehr als eine Ergebniszeile liefert.
Contao 3 bietet - wenn dem Model eine DCA-Struktur zugeordnet ist - außerdem
die Möglichkeit, referenzierte Datensätze automatisch zu laden. Beispielsweise
den Author (`UserModel`) eines Artikels (`ArticleModel`).


## Das Model Objekt


### Instanziierung


Folgend wird eine Instanz von `ArticleModel` erstellt, welche eine bestimmte 
Entität der Tabelle `tl_article` referenziert.

```{.php}
// ArticleModel mit den Daten der Entität id=5 erstellen
$objArticleModel = \ArticleModel::findByPk(5);
 
// ArticleModel mit den Daten der Entität alias='contact' erstellen
$objArticleModel = \ArticleModel::findByIdOrAlias('contact');
// alternativ
$objArticleModel = \ArticleModel::findOneBy('alias','contact');
// alternativ
$objArticleModel = \ArticleModel::findOneByAlias('contact');
```

Die oben verwendeten Methoden sind durch die `\Contao\Model` Klasse 
implementiert. Jedes Model kann zusätzlich in seiner Klasse weitere Constraints
in Methoden kapseln, z.B. `ArticleModel::findPublishedById()`.
Nahezu alle *findBy*-Methoden unterstützen als letzten Parameter ein Array mit
zusätzlichen Parametern, siehe [Methode find()](#methode-findarrdata).


### Virtuelle Methoden

Die oben verwendete `findOneByAlias()` ist eine virtuelle Methode, um auf das
*alias* Feld zu referenzieren. Diese Methoden stehen automatisch über Magic-
Methoden für alle Felder der Tabelle zur Verfügung. Best practice ist es aber,
`findOneBy($column, $value)` zu nutzen.


### Model-Registry

Contao besitzt seit Version 3.2 eine *Model-Registry*. Das bedeutet, dass immer
dieselbe Instanz eines Models zurückgegeben wird, sofern der Primärschlüssel 
übereinstimmt. 

```{.php}
$objArticle = \ArticleModel::findByPk(1);
$objArticle2 = \ArticleModel::findByPk(1);

var_dump($objArticle === $objArticle2); // true

echo $objArticle->title; // Home
$objArticle2->title = 'Home2';
echo $objArticle->title; // Home2
```

Das ist besonders wichtig, wenn Änderungen im Model vorgenommen werden.
Sollen Änderungen nur lokal verfügbar sein, muss eine Kopie der Instanz 
erzeugt werden:

```{.php}
$objArticle = \ArticleModel::findByPk(1);
echo $objArticle->title; // Home

$objArticle2 = clone $objArticle;
$objArticle2->title = 'Home2';
echo $objArticle->title; // Home
```


### Die *protected*-Methode `find($arrOptions)`

Implizit arbeiten alle *findBy*-Methoden mit `find()`.
Die Methode akzeptiert ein Array mit folgenden Werten:

<table>
	<tr>
		<th>Schlüssel</th>
		<th>Typ</th>
		<th>Beschreibung</th>
	</tr>
	<tr>
		<td>column</td>
		<td>mixed</td>
		<td>
			Es gibt zwei Möglichkeiten, die Tabellenspalten anzugeben:<br>
			Als String, z.B. <code>alias</code><br>
			Als Array, z.B. <code>array('tl_article.alias=?')</code><br>
			<br>
			Wird ein String übergeben, konvertiert Contao diesen automatisch zu
			einem entsprechenden Array und ergänzt Tabelle und Operator.
			Beim Array sollte darauf geachtet werden, dass auch die Tabelle
			angegeben wird, da bei referenzierten Datensätzen sonst ggf.
			Fehler wegen duplikaten Spaltennamen auftreten können.
		</td>
	</tr>
	<tr>
		<td>value</td>
		<td>mixed</td>
		<td>Ein Array sollte übergeben werden, falls in mehreren Spalten
		gesucht wird. Ansonsten reicht die Übergabe des einzelnen Wertes.</td>
	</tr>
	<tr>
		<td>limit</td>
		<td>integer</td>
		<td>Beschränkt die Ergebnismenge (LIMIT)</td>
	</tr>
	<tr>
		<td>offset</td>
		<td>integer</td>
		<td>Offset einer beschränkten Ergebnismenge (LIMIT)</td>
	</tr>
	<tr>
		<td>order</td>
		<td>string</td>
		<td>Sortierung der Ergebnismenge (ORDER BY)</td>
	</tr>
	<tr>
		<td>eager</td>
		<td>boolean</td>
		<td>Versucht referenzierte Datensätze durch einen OUTER JOIN zu
		laden.</td>
	</tr>
	<tr>
		<td>return</td>
		<td>string</td>
		<td>Bei Übergabe von <i>Model</i> wird eine Instanz des ersten Resultats
		zurückgegeben, ansonsten immer eine Model-Collection.</td>
	</tr>
</table>


### Getter & Setter

Um auf den Wert einer Spalte der Entität zuzugreifen, benutzt Contao die 
*Magic-Methods* `__get($key)` und `__set($key, $value)`. Diese werden von 
PHP immer dann aufgerufen, wenn der Zugriff auf ein nicht existierendes 
Klassen-Attribut erfolgt. Contao gibt dann die Werte des Datensatzes zurück, 
bzw. setzt diese.

**ACHTUNG:** Es können beliebige Spalten im Model gesetzt werden, gespeichert
werden nur Attribute, für die eine Spalte in der Datenbank-Tabelle vorhanden ist.

``` {.php}
// Titel des Artikels ausgeben
echo $objArticleModel->title;
// Ausgabe: Mein Artikel

// Ändern des Titels
$objArticelModel->title = "Mein besonderer Artikel";
$objArticelModel->something_else = "AnyValue";
$objArticleModel->save();
// Speichert die Änderung des Datensatzes in die Datenbank
// *something_else* wurde nicht gespeichert, da es keine gleichnamige Spalte gibt.
```


### Weitere relevante Methoden


#### Die Methode `row()` 

Gibt alle Werte des Datensatzes als assoziatives Array zurück.
```{.php} 
print_r($objArticelModel->row());
// Array (
//           [id] => 12,
//           [pid] => 1,
//           [title] => Mein besonderer Artikel
//           [tstamp] => 123456,
// ...
```


#### Die Methode `setRow(array $values)`

Setzt alle Werte des Datensatzes anhand des übergebenen assoziativen Arrays
```{.php} 
$objArticelModel->setRow(array
(
  'id' => 12,
  'pid' => 1,
  'tstamp' => 123999,
  'title' => 'Mein neuer Name',
  // ... more attributes
));
```
**ACHTUNG:** Bei Verwendung von `setRow` werden die Model-Daten direkt
überschrieben und die Felder nicht als "zu speichern" markiert! Dies
ist nur sinnvoll, um ein Model aus einem bestehenden Datensatz zu erzeugen.


#### Die Methode `save()`

Speichert alle Änderungen in der Datenbank.
Es werden nur Attribute gespeichert, für die eine Spalte in der Datenbank-
Tabelle vorhanden ist.


#### Die statische Methode `countBy($varColumn=null, $varValue=null)`

Gibt die Anzahl zutreffender Datensätze zurück. Die möglichen Werte für
`$varColumn` und `$varValue` entsprechen dabei den entsprechenden Optionen
der `find()`-Methode.

```{.php}
echo ArticelModel::countBy('pid', 2);
// 2
```


#### Die statische Methode `countAll()`

Gibt die Anzahl aller Datensätze der Tabelle zurück.


### preSave / preFind / postFind

Die Methoden `preSave`, `preFind`, `postFind` können von einer Kindklasse
überschrieben werden, um zusätzliche Logik  an den entsprechenden Stellen
einzufügen.


## Collection Objekt

### Instanziierung

Eine `Collection` Instanz wird durch `Model::findBy()` (bzw. `Model::findAll()`
usw.) instanziiert.

```{.php}
// Finde alle Artikel WHERE pid=2
$objArticles = \ArticleModel::findByPid(2);
// alternativ
$objArticles = \ArticleModel::findBy('pid', 2);
// alternativ
$objArticles = \ArticleModel::findAll(
	array
	(
		'column' => 'pid',
		'value' => 2
	)
);

// Finde alle Artikel WHERE pid=2 AND published='1'
$objArticles = \ArticleModel::findBy(
	array('pid=?', 'published=?'),
	array(2, '1')
);
```


### Zugriff

**ACHTUNG**: Es gibt keine leere *Collection*! Werden keine Datensätze gefunden,
ist der Rückgabewert von `findBy()` bzw. `findAll()` gleich `null`!
Es ist **kein** *Collection* Objekt!

```{.php}
// Fetch all published Articles
$objArticles = \ArticleModel::findBy('published', '1');

if (null === $objArticles) {
	echo 'Keine Artikel gefunden.';
} else {
	echo $objArticles->count().' Artikel gefunden.';
}

// Verwenden des IteratorAggregate interface
foreach($objArticles as $objArticle) {
	echo $objArticle->title.'<br>';
}

// Verwenden der Iterator-Methoden
$objArticles->reset();
while($objArticles->next()) {
	echo $objArticles->title.'<br>';
}

```

**HINWEIS:** Es wird empfohlen, die *foreach*-Variante zu verwenden, da deren
Position nicht vom internen Zähler der *Collection* abhängig ist.


## Referenzierte Datensätze

Ein Contao *Model* kann auf referenzierte Datensätze zugreifen. Damit Contao
diese Referenzen auflösen kann, muss dem *Model* ein *DCA* zugeordnet sein,
welches normalerweise identisch mit dem Namen der Tabelle ist.

```{.php}
class ArticleModel extends \Model
{
	/**
	 * Table name
	 * @var string
	 */
	protected static $strTable = 'tl_article';
...
```

Im *DCA* wird die Relation anhand von `foreignKey` und `relation` definiert:
```{.php}
$GLOBALS['TL_DCA']['tl_article'] = array
(
...
// Fields
	'fields' => array
	(
		'pid' => array
		(
			'sql'                     => "int(10) unsigned NOT NULL default '0'",
			// Relation definition for `pid`
			'foreignKey'              => 'tl_page.title',
			'relation'                => array('type'=>'belongsTo', 'load'=>'lazy')
		),
		'author' => array
		(
			'label'                   => &$GLOBALS['TL_LANG']['tl_article']['author'],
			'exclude'                 => true,
			'inputType'               => 'select',
			'sql'                     => "int(10) unsigned NOT NULL default '0'",
            // Relation definition for `author`
			'foreignKey'              => 'tl_user.name',
			'relation'                => array('type'=>'hasOne', 'load'=>'eager')
		),
```
Im oberen Beispiel wird eine Relation für die Spalte `pid` auf die Tabelle 
`tl_page` festgelegt. Die Datensätze werden *lazy*, d.h. erst bei Bedarf 
geladen. Die Relation für `author` zur Tabelle `tl_user` wird dagegen *eager*, 
also durch einen SQL-JOIN geladen.

Contao versucht die Klasse des referenzierten Models anhand des Namens der 
Tabelle zu finden. Bsp.: 
```
tl_page => \PageModel
tl_form_field => \FormFieldModel
```
Folgt die Implementierung nicht dieser Konvention oder befindet sich die 
Model-Klasse nicht im globalen Namenspace, muss die entsprechende Klasse 
konfiguriert werden:
```{.php}
$GLOBALS['TL_MODELS']['tl_my_table'] = 'Vendor\Models\MyTable';
```


### Relations-Typen

<table>
	<tr>
		<th>Schlüssel</th>
		<th>Wert</th>
		<th>Beschreibung</th>
	</tr>
	<tr>
		<td>load</td>
		<td>eager</td>
		<td>Wird ein in Beziehung (nur *hasOne* oder *belongsTo*) stehendes
		Objekt „eager“ geladen, erstellt der QueryBuilder automatisch ein
		OUTER JOIN-Query und lädt die Objekte in einer einzigen Datenbank-
		Abfrage.</td>
	</tr>
	<tr>
		<td>load</td>
		<td>lazy</td>
		<td>Wird ein in Beziehung stehendes Objekt „lazy“ geladen, wird es 
		erst auf Anfrage in einer separaten Datenbank-Abfrage nachgeladen.</td>
	</tr>
	<tr>
		<th>Schlüssel</th>
		<th>Wert</th>
		<th>Beschreibung</th>
	</tr>
	<tr>
		<td>type</td>
		<td>belongsTo</td>
		<td>Referenz auf einen Elterndatensatz (z.B. pid)</td>
	</tr>
	<tr>
		<td>type</td>
		<td>belongsToMany</td>
		<td>Referenz auf mehrere Elterndatensätze (z.B. serialized)</td>
	</tr>
	<tr>
		<td>type</td>
		<td>hasOne</td>
		<td>Referenz auf einen Kinddatensatz (z.B. Artikel hat einen Autor)</td>
	</tr>
	<tr>
		<td>type</td>
		<td>hasMany</td>
		<td>Referenz auf mehrere Kinddatensätze (z.B. Galerie hat mehrere
		Bilder)</td>
	</tr>
	<tr>
		<th>Schlüssel</th>
		<th>Wert</th>
		<th>Beschreibung</th>
	</tr>
	<tr>
		<td>table</td>
		<td><i>string</i></td>
		<td>Der Name der verknüpften Tabelle, falls <code>foreignKey</code>
		bereits anderweitig verwendet wird. Vorsicht: bis Contao 3.2.2 musste
		immer ein <code>foreignKey</code> gesetzt sein!</td>
	</tr>
	<tr>
		<td>field</td>
		<td><i>string</i></td>
		<td>Name des Tabellenfeldes, falls sich die Relation nicht auf 
		<code>id</code> (den Standard-Primärschlüssel) bezieht.</td>
	</tr>
</table>


## Weiterführende Informationen

* [API-Doku Model Klasse](http://api.contao.org/classes/Contao.Model.html)
* [API-Doku Collection Klasse](http://api.contao.org/classes/Contao.Model.Collection.html)
* [Foliensatz Entwickler-Workshop der Konferenz 2012](https://contao.org/files/conference/2012/papers/Entwickler-Workshop.pdf)
