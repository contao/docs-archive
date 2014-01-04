# Models

Ein *Model* repräsentiert einen Datensatz aus einer Tabelle (Entität). Models 
ersetzen weitgehend SQL-Statements und wrappen diese in Objekte und darüber 
hinaus bieten sie viele weitere Vorteile.
Mehrere Models werden durch eine *Collection* referenziert, dies entspricht 
einer SQL-Abfrage die mehr als eine Ergebniszeile liefert.
Contao3 bietet - wenn dem Model eine DCA-Struktur zugeordnet ist - etwas Magic 
um referenzierte Datensätze zu laden. Beispiel: Der Author (`UserModel`) 
eines Artikels (`ArticleModel`).


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
implementiert. Sie können intern von einem speziellen Model wie dem 
*ArticleModel* genutzt werden um weitere Constraints in Methoden zu kapseln.

Bsp.: `ArticleModel::findPublishedById()`.
*findOneByAlias()* ist eine virtuelle Methode um auf das *alias* Feld zu
referenzieren. Diese Methoden existieren für jedes Feld der Tabelle.
Bsp: `findOneByName()`. Best practice ist `findOneBy($col, $val)` zu nutzen.
Alle anderen *find*-Methoden benutzen implizit die protected-Method *find()*.
Nahezu alle dieser Methoden unterstützen als letzten Parameter ein Subset
des `$arrData` Arrays, siehe [Methode find()](#methode-findarrdata).


### Model-Registry

Contao besitzt ab Version 3.2 eine *Model-Registry*. Das bedeutet, dass die 
selbe Instanz eines Models zurückgegeben wird, sofern der Primärschlüssel 
übereinstimmt. 

```{.php}
$objArticle = \ArticleModel::findByPk(1);
$objArticle2 = \ArticleModel::findByPk(1);

var_dump($objArticle === $objArticle2); // true

echo $objArticle->title; // Home
$objArticle2->title = 'Home2';
echo $objArticle->title; // Home2
```

Das ist vor allem wichtig, wenn Änderungen im Model vorgenommen werden.
Sollen Änderungen nur *local* verfügbar sein, muss eine Kopie der Instanz 
erzeugt werden:

```{.php}
$objArticle = \ArticleModel::findByPk(1);
echo $objArticle->title; // Home

$objArticle2 = clone $objArticle;
$objArticle2->title = 'Home2';
echo $objArticle->title; // Home
```


### Methode: protected `find($arrOptions)`
Implizit arbeiten alle `find*` Methoden mit `find()`.
Die Methode akzeptiert ein Array mit folgenden Array-Keys:

<table>
	<tr>
		<th>Schlüssel</th>
		<th>Typ</th>
		<th>Beschreibung</th>
	<tr>
	<tr>
		<td>column</td>
		<td>array</td>
		<td>Feld(er) zur Selektion (WHERE)</td>
	</tr>
	<tr>
		<td>value</td>
		<td>array</td>
		<td>Wert(e) zur Selektion (WHERE)</td>
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
		<td>bool</td>
		<td>Lädt die referenzierten Datensätze durch einen JOIN</td>
	</tr>
	<tr>
		<td>return</td>
		<td>string</td>
		<td>Gültige Werte: Model,Collection Legt fest, ob eine 
		Collection-Instanz (default) oder eine Model-Instanz zurück gegeben 
		wird.</td>
	</tr>
</table>


### Getter & Setter
Um auf den Wert einer Spalte einer Entität zuzugreifen benutzt Contao die 
*Magic-Methods* `__get($key)` und `__set($key, $value)`. Diese werden von 
PHP immer dann aufgerufen, wenn der Zugriff auf ein nicht existierendes 
Klassen-Attribut erfolgt. Contao gibt dann die Werte des Datensatzes zurück, 
bzw. setzt diese.

Achtung: Es werden nur Attribute gespeichert, die eine Entsprechung in der
Datenbank-Tabelle haben.

``` {.php}
// Titel des Artikels ausgeben
echo $objArticleModel->title;
// Ausgabe: Mein Artikel

// Verändern/setzen des Titels
$objectArticelModel->title = "Mein besonderer Artikel";
$objectArticelModel->fld_not_exists_in_db = "AnyValue";
$objectArticleModel->save(); // speichert die Änderung des Datensatzes in die Datenbank
// fld_not_exists_in_db wurde nicht festgeschrieben, da es keine gleichnamige Spalte gibt.
```


### Weitere relevante Methoden


#### `row()` 
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


#### array `setRow()`
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


#### `save()`
Speichert alle Änderungen in der Datenbank.
Es werden nur Attribute gespeichert, die eine gleichnamige Splate in der
Datenbank-Tabelle haben.


#### static `countBy($strColumn=null, $varValue=null)`
Gibt die Anzahl der Datensätzen, die in der Spalte `$strColumn` den Wert 
`$strValue` enthalten, zurück.

```{.php}
echo ArticelModel::countBy('pid', 2);
// 2
```


#### `countAll()`
Gibt die Anzahl aller Datensätze der Tabelle zurück.


### preSave / preFind / postFind

Die statischen Methoden `preSave`, `preFind`, `postFind` können von einer 
konkreten Model Implementierung überschrieben werden um zusätzliche Logik 
an den entsprechenden Stellen einzufügen.


## Collection Objekt


### Instanziierung
Eine `Collection` Instanz wird durch die `find($arr)` Methode
(bzw. `findAll($arr)`, `findBy($col, $val)`, usw.) instanziiert.

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
// alternativ
$objArticles = \ArticleModel::find(
  array
  (
      'return' => 'Collection',
      'column' => 'pid',
      'value' => 2
  )
);

// Finde alle Artikel WHERE pid=2 AND published="1"
$objArticles = \ArticleModel::find(
  array
  (
      'return' => 'Collection',
      'column' => array('pid=>?', 'published=>?'),
      'value' => array(2, '1')
  )
);
```


### Zugriff

**ACHTUNG**: Es gibt keine leere *Collection*! Werden keine Datensätze gefunden,
ist der Rückgabewert von `find()` bzw. `findAll()` gleich `null`!
Es ist **kein** *Collection* Object!

```{.php}
// Fetch all published Articles
$objArticles = \ArticleModel::findAll(array('column'=>'published', 'value'=>'1'));

echo "Found ".$objArticles->count().' articles <br>';

// Verwenden des IteratorAggregate interface
foreach($objArticles as $objArticle) {
	echo $objArticle->title.'<br>';
}

// Verwenden der Iterator-Methoden
while($objArticles->next()) {
	echo $objArticles->current()->title.'<br>';
}

```


## Referenzierte Datensätze

Ein Contao *Model* kann auf referenzierte Datensätze zugreifen. Beispiel: 
Artikel->Autor. Damit Contao diese Referenzen auflösen kann, muss dem *Model* 
ein `DCA` zugeordnet sein. Sie ist normalerweise identisch mit dem Namen 
der Tabelle.

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

Im `DCA` wird die Relation anhand der `foreignKey` und `relation` Keys definiert:
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
$GLOBALS['TL_MODELS']['tl_my_table'] = 'MyNamespace\TblModel';
```


### Relations-Typen


#### load
<table>
	<tr>
		<td><b>eager</b></td>
        <td>Wird ein in Beziehung (nur hasOne, belongsTo) stehendes Objekt „eager“ geladen, erstellt 
        der QueryBuilder automatisch ein JOIN-Query und lädt die Objekte in 
        einer einzigen Datenbank-Abfrage.</td>
    </tr>
	<tr>
		<td><b>lazy</b></td>
    	<td>Wird ein in Beziehung stehendes Objekt „lazy“ geladen, wird es 
    	erst auf Anfrage in einer separaten Datenbank-Abfrage nachgeladen.</td>
    </tr>
</table>


#### type
<table>
	<tr>
		<td><b>belongsTo</b></td>
        <td>Referenz auf einen Elterndatensatz (z.B. pid)</td>
    </tr>
	<tr>
		<td><b>belongsToMany</b></td>
        <td> Referenz auf mehrere Elterndatensätze (z.B. serialized)</td>
    </tr>
	<tr>
		<td><b>hasOne</b></td>
        <td> Referenz auf ein Kinddatensatz (z.B. Artikel hat einen Autor)</td>
    </tr>
	<tr>
		<td><b>hasMany</b></td>
        <td>Referenz auf mehrere Kinddatensätze (z.B. Galerie hat mehrere Bilder)</td>
    </tr>
</table>


## Weiterführende Informationen

* [API-Doku Model Klasse](http://api.contao.org/classes/Contao.Model.html)
* [API-Doku Collection Klasse](http://api.contao.org/classes/Contao.Model.Collection.html)
* [Foliensatz Entwickler-Workshop der Konferenz 2012](https://contao.org/files/conference/2012/papers/Entwickler-Workshop.pdf)
