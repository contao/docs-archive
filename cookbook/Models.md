# Models

Ein *Model* repräsentiert einen Datensatz aue einer Tabelle (Entität). Models ersetzen weitgehend SQL-Statements und wrappen diese in Objekte und darüber hinaus bieten sie viele weitere Vorteile.
Mehrere Models werden durch eine *Collection* referenziert, dies entspricht einer SQL-Abfrage die mehr als eine Ergebniszeile liefert.
Contao3 bietet - wenn dem Model eine DCA-Struktur zugeordnet ist - etwas Magic um referenzierte Datensätze zu laden. Beispiel: Der Author (`UserModel`) eines Artikels (`ArticleModel`).

## Model Object

### Instanziierung 

Folgend wird eine Instanz von `ArticleModel` erstellt, welche eine bestimmte Entität der Tabelle tl_article referenziert.

``` {.php}
// ArticleModel mit den Daten der Entität id=5 erstellen
$objArticleModel = \ArticleModel::findByPk(5);
 
// ArticleModel mit den Daten der Entität alias='contact' erstellen
$objArticleModel = \ArticleModel::findByIdOrAlias('contact');
// alternativ
$objArticleModel = \ArticleModel::findOneBy('alias','contact');
// alternativ
$objArticleModel = \ArticleModel::findOneByAlias('contact');
// alternativ
$objArticleModel = \ArticleModel::find(
  array (
    'limit'   => 1,
    'column'  => 'alias',     // mehrere Spalten durch array() möglich, dann muss nach den Feldnamen =? eingefügt werden (z.B. 'alias =?')
    'value'   => 'contact',   // mehrere Werte durch array() möglich, Reiehenfolge analog 'column'
    'return   => 'Model'
  )
);
```

Die oben verwendeten Methoden sind durch die `\Contao\Model` Klasse implementiert.
Sie können intern von einem speziellen Model wie das *ArticleModel* genutzt werden um weitere Constraints in Methoden zu kapseln.

Bsp.: `ArticleModel::findPublishedById()`.
*findOneByAlias()* ist eine virtuelle Methode um auf das *alias* Feld zu referenzieren.
Diese Methoden existieren für jedes Feld der Tabelle. Bsp: `findOneByName()`.
Best practice ist `findOneBy($col, $val)` zu nutzen.
Die statische Basismethode `find($arrData)` ermöglicht eine genaue Spezifizierung der Anfrage. Alle anderen *find*-Methoden benutzen implizit *find()*.


### Methode: find($arrData)
Die Methode akzeptiert ein Array mit folgenden Array-Keys:

| key       |  type  | Beschreibung |
|--         | --     | -- |
| column	| array  | Feld(er) zur Selektion (WHERE) |
| value     | array  | Wert(e) zur Selektion (WHERE)  |
| limit     | int	 | Beschränkt die Ergebnismenge (LIMIT) |
| offset    | int    | Offset einer beschränkten Ergebnismenge (LIMIT) |
| order     | string | Sortierung der Ergebnismenge (ORDER BY) |
| eager     | bool   | Lädt die referenzierten Datensätze durch einen JOIN |
| return    | string | Gültige Werte: Model,Collection Legt fest, ob eine Collection-Intanz (default) oder eine Model-Instanz zurück gegeben wird. |

### Getter & Setter
Um auf den Wert einer Spalte einer Entität zuzugreifen benutzt Contao die *Magic-Methods* `__get($key)` und `__set($key, $value)`. Diese werden von PHP immer dann aufgerufen, wenn der Zugriff auf ein nicht existierendes Klassen-Attribut erfolgt. Contao gibt dann die Werte des Datensatzes zurück, bzw. setzt diese.

``` {.php}
// Titel des Artikels ausgeben
echo $objArticleModel->title;
// Ausgabe: Mein Artikel

// Verändern/setzen des Titels
$objectArticelModel->title = "Mein besonderer Artikel";
$objectArticleModel->save(); // speichert die Änderung des Datensatzes in die Datenbank
```

### Weitere relevante Methoden

#### `row()` 
Gibt alle Werte des Datensatzes als assoziatives Array zurück.
``` {.php} 
print_r($objectArticelModel->row());
// Array (
//           [id] => 12,
//           [pid] => 1,
//           [title] => Mein besonderer Artikel
//           [tstamp] => 123456,
// ...
```

#### array `setRow()`
Setzt alle Werte des Datensatzes anhand des übergebenen assoziativen Arrays
``` {.php} 
$objectArticelModel->setRow(array
(
  'id' => 12,
  'pid' => 1,
  'tstamp' => 123999,
  'title' => 'Mein neuer Name',
  // ... more attributes
));
```

#### `save($blnForceInsert=false)`
Speichert alle Änderungen in der Datenbank.
Der optionale Parameter `$blnForceInsert` erzeugt einen neuen Datensatz, selbst wenn das Attribut `$id` gesetzt ist. 

#### static `countBy($strColumn=null, $varValue=null)`
Gibt die Anzahl der Datensätzen, die in der Spalte `$strColumn` den Wert `SstrValue` enthalten zurück. 

``` {.php}
// Zählt die Anzahl der Datensätze die in der Spalte pid den Wert 2 enthalten
echo ArticelModel::countBy('pid', 2);
// 2
```

`countAll()`
Gibt die Anzahl aller Datensätze der Tabelle zurück.

### preSave / preFind / postFind

Die statischen Methoden `preSave`, `preFind`, `postFind` können von einer konkreten Model Implementierung überschrieben werden um zusätzliche Logik an den entsprechenden Stellen einzufügen.


## Collection Object

### Instanziierung
Eine `Collection` Instanz wird durch die `find($arr)` Methode  (bzw. `findAll($arr)`, `findBy($col, $val)`, usw.) instanziiert.   

``` {.php}
// Finde alle Artikel WHERE pid=2
$objArticles = \ArticleModel::findByPid(2);
// alternativ
$objArticles = \ArticleModel::findBy('pid',2);
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
