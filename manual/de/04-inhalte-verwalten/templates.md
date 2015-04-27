## Templates

Ein Template enthält meist HTML und PHP code. Es wird zur Ausgabe von Inhalten 
eines Moduls oder Inhaltelements etc. verwendet. Beispielsweise gibt das 
Template `news_full.html5` eine vollständige Nachricht aus, während das Template 
`news_short.html5` nur einen Teil davon anzeigt.

Templates befinden sich direkt in den dazugehören Modulen. Das `news_full.html5` 
Template befindet sich beispielsweise in `system/modules/news/templates/news`.

Falls diese Datei direkt in diesem Ordner bearbeitet wird, **gehen die Änderungen** 
bei einem nächsten Update von Contao **verloren**. Um dies zu vermeiden, 
Templates können im Backend bearbeitet werden. Dabei wird die Datei kopiert um 
Änderungen während einem Update nicht zu verlieren.

![](images/templates.jpg?raw=true)

Unter dem Menüpunkt *Templates* können die Dateien bearbeitet und in Ordnern 
abgelegt werden. Ordner müssen wie unter [Theme-Bestandteile][1] beschrieben 
einem Theme zugewiesen sein.

Ein Template gehört zu einem Modul, einem Inhaltselement, einem Formular oder 
anderen Komponenten. Sie werden zur einfacheren Erkennung deshalb meist mit 
einem Präfix versehen. Beispielsweise deutet `j_` auf jQuery oder `nl_` auf 
ein Newsletter-Template.


### Template-Vererbung

Template-Vererbung erlaubt, ein Template basierend auf einem anderen Template 
aufzubauen. Dies bedeutet, ein Template (Kind) fügt Inhalt in ein zweites 
Template (Eltern) ein.

Damit Inhalte in einem Eltern-Template angepasst werden können, muss sich der 
Inhalt innerhalb eines `block`-Elements befinden.

Ein Block ist wie folgt aufgebaut:

```php
<?php $this->block('name_des_blocks'); ?>

  // Block-Inhalt

<?php $this->endblock(); ?>
```

Das folgende Beispiel zeigt ein Template bei welchem der `head`-Tag als eigener 
Block definiert wurde.

Template `fe_page.html5`:

```html
<!DOCTYPE html>
<html>
<head>
  <?php $this->block('head'); ?>
    <title><?php echo $this->title; ?></title>
    <link rel="stylesheet" href="style.css">
  <?php $this->endblock(); ?>
</head>
<body>
  ...
</body>
</html>
```

Im Kindtemplate `fe_custom.html` wird zusätzlich zum bisherigen Inhalt 
noch ein CSS style sheet in das übergeordnete Template eingefügt.

Template `fe_custom.html5`:

```html
<?php $this->extend('fe_page'); ?>

<?php $this->block('head'); ?>
  <?php $this->parent(); ?>
  <link rel="stylesheet" href="style_2.css">
<?php $this->endblock(); ?>
```

* Die Funktion `extend()` definiert das übergeordnete Template.
* Die Funktion `parent()` übernimmt den Inhalt des übergeordneten Template.

Die Ausgabe des `fe_custom.html5` Template sieht danach so aus:

```html
<!DOCTYPE html>
<html>
<head>
  <title>A title</title>
  <link rel="stylesheet" href="style.css">
  <link rel="stylesheet" href="style_2.css">
</head>
<body>
  ...
</body>
</html>
```


### Templates mischen

Mit Hilfe der `insert()`-Funktion kann ein Template in ein anderes Template
einfügt werden.

```php
<?php $this->insert('template_name'); ?>
```

Die `insert()`-Funktion akzeptiert ausserdem auch die Übergabe von zusätzlichen 
Variablen als zweiten Parameter.

```php
<?php $this->insert('template_name', array('key'=>'value')); ?>
```

Im folgenden Beispiel fügen wir den Inhalt des Templates `image-copyright.html5` 
in das Template `image.html5` ein.

Das Template `image.html5` enthält lediglich einen `img`-Tag und die 
`insert()`-Funktion.

Template `image.html5`:

```html
<img src="<?php echo $this->src; ?>" alt="<?php echo $this->alt; ?>" />
<?php $this->insert('image-copyright', array('name'=>'Donna Evans', 'license'=>'Creative Commons')); ?>
```

Das `image-copyright.html5` Template enthält einen `small`-Tag welcher nach dem
`img`-Tag im `image.html5` Template eingefügt werden soll. Die Variabeln `name` 
und `license` werden durch die Parameter der `insert()`-Funktion ersetzt.

Template `image-copyright.html5`:

```html
<small>Fotografiert von <?php echo $this->name; ?>, lizenziert als <?php echo $this->license; ?></small>
```

Die Ausgabe des `image.html5` sieht danach folgendermassen aus:

```html
<img src="files/images/house.jpg" alt="Ein kleines Haus in England" />
<small>Fotografiert von Donna Evans, lizenziert als Creative Commons</small>
```


[1]: ../03-seiten-verwalten/themes.md#theme-bestandteile