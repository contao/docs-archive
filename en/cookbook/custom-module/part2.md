#Create a custom Contao module – part two
  
  
![Create a custom TYPOlight module CD Collection](http://blog.qzminski.com/wp-content/uploads/2010/04/introimg.jpg)

In this part of CD Collection module tutorial, I will show you how to create the most important part of our module – the Data Container Array. At a glance, it is a table configuration array, which tells Contao how to render module’s back end form.

Just like the configuration files, DCA files are loaded when the Contao is initialized. It allows you to overwrite existing settings of other modules. As you know from the previous part of the tutorial, modules are loaded in the alphabetical order. Thus, if you want to add a new field to the news module, you don’t need to modify any of the news files. But that’s the subject for another tutorial.


##File structure

The DCA file must be located in /cd_collection/dca/ folder and have the same name as the table definied in the module config:

```php
// Back end module
array_insert($GLOBALS['BE_MOD']['content'], 3, array
(
  'cd_collection' => array
  (
    'tables' => array('tl_cds_category', 'tl_cds'),
    'icon'   => 'system/modules/cd_collection/html/icon.gif'
  )
));

```

Please create two files called tl\_cds\_category.php and tl\_cds.php in dca folder.


##Inside DCA

The data container array has usually the following structure:

```php
<?php

$GLOBALS['TL_DCA']['tl_table'] = array
(

  'config' => array
  (
    // dca config settings go here
  ),

  'list' => array
  (
    // all settings that are applied to records listing
    // we can define here: sorting, panel layout (filter, search, limit fields), label format, global operations, operations on each record
  ),

  'palettes' => array
  (
    // palettes settings
  ),

  'fields' => array
  (
    // fields that are visible in back end form
  )
);

?>
```

As you can see it is one big nested array. First part, the config, contains basic settings like data container type or table relationship (child/parent). The list array is usually divided into four sections: sotring, label, global_operations, operations. Each of them is also an array. Next, the palettes – a palette defines the order of displaying form fields; it is also possible to group them into sections (available from 2.7.0). Finally, the fields is an array that holds information about our form fields.

All of the config options are available on the [official website](http://www.typolight.org/dca.html).

That is all of the basic theory, let’s get to work!


##DCA config

Open tl\_cds\_category.php and put the following content:


```php
<?php

$GLOBALS['TL_DCA']['tl_cds_category'] = array
(

  // Config
  'config' => array
  (
    'dataContainer'               => 'Table',
    'ctable'                      => array('tl_cds'),
    'switchToEdit'                => true
 ),
//...

```


As a data container we have defined table, because our module will use the MySQL database tables.  
 
The ‘ctable’ is a shortcut from ‘children table’. In the [previous part](http://blog.qzminski.com/2010/04/create-a-custom-typolight-module-part-one/), we assumed that tl_cds is our child table.

SwitchToEdit key, if true, activates the “save and edit” buton when a new record is added:


![Save and edit button](http://blog.qzminski.com/wp-content/uploads/2010/04/save_and_edit.jpg)

However, this button is available only when the sorting mode is 4.



##DCA list


The list array is used to maintain the homepage of our module. Its purpose is to set up the user interface and provide a listing of records. It consists of four arrays that I will describe in a moment. Meanwhile I advise you to open a [developer’s guide](http://www.typolight.org/reference.html) to make you see better what I am talking about.


###Sorting

Okay, so the first array is called sorting. As its name points out, it is used to define the settings for displaying our records. Put the following code into the file:

```php
  // List
  'list' => array
  (
    'sorting' => array
    (
      'mode'                    => 1,
      'fields'                  => array('title'),
      'flag'                    => 1,
      'panelLayout'             => 'search,limit'
    ),
//...
```
Mode set to 1 defines that records are sorted by a fixed field, which is defined in the next line. Here we choose the title of the category to be base for our sorting. Flag determines how records are sorted; 1 means “sort by initial letter ascending”, in other words – alphabetically. At the end of this subarray we define panel layout, which features search box and record limit dropdown.



![Panel layout](http://blog.qzminski.com/wp-content/uploads/2010/04/panelLayout.jpg)

*Panel layout of the Modules*




###Label

The label array is also a child of the list array. It is used to define the record’s label format. You might notice that this is similar to php sprintf() function. To better visualize the analogy, below code works like 
```php
sprintf(format, fields)
```

Paste the following code:

```php
    'label' => array
    (
      'fields'                  => array('title'),
      'format'                  => '%s'
    ),
//...
```

I hope this code is clear to you. It simply gets the title field from the database and displays it.



###Global operations

…are the functions that can be applied to multiple records same time. A perfect example is the edit multiple function, which we’ll implement into our module:

```php
'global_operations' => array
    (
      'all' => array
      (
        'label'               => &$GLOBALS['TL_LANG']['MSC']['all'],
        'href'                => 'act=select',
        'class'               => 'header_edit_all',
        'attributes'          => 'onclick="Backend.getScrollOffset();"'
      )
    ),
//...
```


![Global operations](http://blog.qzminski.com/wp-content/uploads/2010/04/global_operations.jpg)

*The above code will add the "Edit multiple" link*



###Operations

This array defines which operations will be available for each record. Put the following code:

```php
    'operations' => array
    (
      'edit' => array
      (
        'label'               => &$GLOBALS['TL_LANG']['tl_cds_category']['edit'],
        'href'                => 'table=tl_cds',
        'icon'                => 'edit.gif',
      ),
      'copy' => array
      (
        'label'               => &$GLOBALS['TL_LANG']['tl_cds_category']['copy'],
        'href'                => 'act=copy',
        'icon'                => 'copy.gif',
      ),
      'delete' => array
      (
        'label'               => &$GLOBALS['TL_LANG']['tl_cds_category']['delete'],
        'href'                => 'act=delete',
        'icon'                => 'delete.gif',
        'attributes'          => 'onclick="if (!confirm(\'' . $GLOBALS['TL_LANG']['MSC']['deleteConfirm'] . '\')) return false; Backend.getScrollOffset();"',
      ),
      'show' => array
      (
        'label'               => &$GLOBALS['TL_LANG']['tl_cds_category']['show'],
        'href'                => 'act=show',
        'icon'                => 'show.gif'
      )
    )
  ), // end of list array
//...
```

I think the code is self-explanatory. We have added four basic functions that come in almost every module of Contao.

Note that the edit array takes as href key other value than a typical (one-table) module – and that’s because we use two tables in our cd collection. Thus, when you click the edit button, it will take you to the listing of tl\_cds records!


![Operations](http://blog.qzminski.com/wp-content/uploads/2010/04/operations.jpg)

*Each record can be either edited, copied, removed or simply showed*



##DCA Palettes


*Palettes* array defines how the module’s form should be presented. Since version 2.7 you can group fields into sections, which is a really great usability improvement.


```php
  // Palettes
  'palettes' => array
  (
    'default'                     => '{title_legend},title,description'
  ),
//...
```

As you can guess, the default palette is displayed by default.

A palette is a string of field names which are concatenated with either a semicolon (;) or a comma (,). Whereas the comma is just used to separate the field names, the semicolon indicates the beginning of a new fieldset.

The legends (those expandable and collapsable groups/fieldsets) should be always surrounded with braces – just like {title_legend}. See the image for better explanation:

![Palettes](http://blog.qzminski.com/wp-content/uploads/2010/04/palettes.jpg)


##DCA Fields

The above settings can be copy-pasted (with some little changes) into any of our modules, but fields are always unique for each module and have to be created manually. Put the following code:

```php
  // Fields
  'fields' => array
  (
    'title' => array
    (
      'label'                   => &$GLOBALS['TL_LANG']['tl_cds_category']['title'],
      'inputType'               => 'text',
      'search'                  => true,
      'eval'                    => array('mandatory'=>true, 'maxlength'=>64)
    ),
    'description' => array
    (
      'label'                   => &$GLOBALS['TL_LANG']['tl_cds_category']['description'],
      'inputType'               => 'textarea',
      'eval'                    => array('rte' => 'tinyFlash')
    )
  )
); // end of $GLOBALS['TL_DCA']['tl_cds_category'] array

?>
```

According to our module table in the database, we have added two fields: title and description. Now a little explanation of each of them.

Label and inputType keys are obvious. Label’s value corresponds to the array that we will create in the next part of the tutorial. The search set to true makes the title field available to search via panel layout.

Eval(uation) array configures a particular field in detail. You can e.g. create mandatory fields, add a date picker or define the rich text editor of a textarea.

We set the title to true and its max length to 64, same as the field in a database. Description is a textarea with a lightweight config of a rte.



##tl_cds DCA

Okay, now it’s time to create the data container array for tl\_cds table. It will have a little different config, as it is a child of tl\_cds\_category. Note that Contao is not able to display child records by default, so we are going to use a child_record_callback.


##DCA Config

Open the cd_collection/dca/tl\_cds.php file and put the following content:

```php
<?php

$GLOBALS['TL_DCA']['tl_cds'] = array
  (

  // Config
  'config' => array
  (
    'dataContainer'               => 'Table',
    'ptable'                      => 'tl_cds_category',
  ),
//...
```

Above code is very simple. We define the database table as our data container, and tl\_cds\_category as a parent table.




##DCA List

###Sorting

Now, insert the code:

```php
  // List
  'list' => array
  (
  'sorting' => array
    (
      'mode'                    => 4,
      'fields'                  => array('title'),
      'flag'                    => 1,
      'headerFields'            => array('title', 'description'),
      'panelLayout'             => 'search,limit',
      'child_record_callback'   => array('tl_cds', 'listCds')
    ),
//...
```

The sorting mode is set to 4 – displays the child records of a parent record. However, as I have mentioned before, Contao is not able to list them. Thus, we need to create a new function and assign it to child\_record\_callback. First parameter in array is name of the class, while the second is name of the function. Usually functions are placed at the end of the file, so I will leave it for later.

From version 2.9.0, Contao provides records sorting in mode 4, so we also need to define a flag and the fields. Flag set to 1 means that the records will be sorted by initial letter ascending (from A to Z).

headerFields array defines which fields of parent table are going to be listed in the child module:


![Header fields](http://blog.qzminski.com/wp-content/uploads/2010/04/header_fields.jpg)

*This data is taken from tl\_cds\_category table*


You can see that “My collection of rock cds.” is not on the same height as “description:”. This happens when we display field that is created by rich text editor. By default, rte embeds the text in \<p\> tags. Contao backend’s css applies a 12px bottom margin to all paragraph elements.


###Global operations & operations

Global operations are the same as tl\_cds\_category’s. Operations have just one lil difference – in the edit array, href key takes as value ‘act=edit’, and not ‘table=tl\_cds’.


```php
    'global_operations' => array
    (
      'all' => array
      (
        'label'               => &$GLOBALS['TL_LANG']['MSC']['all'],
        'href'                => 'act=select',
        'class'               => 'header_edit_all',
        'attributes'          => 'onclick="Backend.getScrollOffset();"'
      )
    ),
    'operations' => array
    (
      'edit' => array
      (
        'label'               => &$GLOBALS['TL_LANG']['tl_cds']['edit'],
        'href'                => 'act=edit',
        'icon'                => 'edit.gif'
      ),
      'copy' => array
      (
        'label'               => &$GLOBALS['TL_LANG']['tl_cds']['copy'],
        'href'                => 'act=copy',
        'icon'                => 'copy.gif'
      ),
      'delete' => array
      (
        'label'               => &$GLOBALS['TL_LANG']['tl_cds']['delete'],
        'href'                => 'act=delete',
        'icon'                => 'delete.gif',
        'attributes'          => 'onclick="if (!confirm(\'' . $GLOBALS['TL_LANG']['MSC']['deleteConfirm'] . '\')) return false; Backend.getScrollOffset();"'
      ),
      'show' => array
      (
        'label'               => &$GLOBALS['TL_LANG']['tl_cds']['show'],
        'href'                => 'act=show',
        'icon'                => 'show.gif'
      )
    )
  ), // end of list array
//...

```



##DCA Palettes

It is time to organize our fields and group them into sections. Put the following code after the list array:


```php
  // Palettes
  'palettes' => array
  (
    'default'                     => '{title_legend},title,artist;{image_legend},image;{comment_legend:hide},comment'
  ),
//...
```

Notice that the semicolons are used to seperate the fieldsets. Also, you might notice a new legend element **:hide.** It forces a group to be collapsed by default. Simple yet usfeul.



##DCA Fields

Time for the best part – defining fields :)

We need to create four fields: title, artist, image and comment. Just like in the database.


```php
// Fields
  'fields' => array
  (
    'title' => array
    (
      'label'                   => &$GLOBALS['TL_LANG']['tl_cds']['title'],
      'inputType'               => 'text',
      'search'                  => true,
      'eval'                    => array('mandatory'=>true, 'maxlength'=>64, 'tl_class'=>'w50')
    ),
    'artist' => array
    (
      'label'                   => &$GLOBALS['TL_LANG']['tl_cds']['artist'],
      'inputType'               => 'text',
      'search'                  => true,
      'eval'                    => array('mandatory'=>true, 'maxlength'=>64, 'tl_class'=>'w50')
    ),
    'image' => array
    (
      'label'                   => &$GLOBALS['TL_LANG']['tl_cds']['image'],
      'inputType'               => 'fileTree',
      'eval'                    => array('files'=>true, 'filesOnly'=>true, 'fieldType'=>'radio')
    ),
    'comment' => array
    (
      'label'                   => &$GLOBALS['TL_LANG']['tl_cds']['comment'],
      'inputType'               => 'textarea',
      'eval'                    => array('rte'=>'tinyFlash')
    )
  )
); // end of $GLOBALS['TL_DCA']['tl_cds'] array
//...
```


Step by step:

Title – a normal text input, available for search, with max length of 64 characters. The new thing for you is tl_class. There are 5 input’s classes in Contao that are used for better appearance. All classes can be found [here](http://www.typolight.org/palettes.html).


![Inputs without classes](http://blog.qzminski.com/wp-content/uploads/2010/04/without_classes.jpg)

*Fields without applied classes*


![Fields with classes](http://blog.qzminski.com/wp-content/uploads/2010/04/with_classes.jpg
)

*Fields with applied 'w50' class*


Artist – this field is exact to title’s one.

Image – as input type we define file tree, which will render a file structure of tl_files folder. Additionally, we set the files to true, which causes that both files and folders will be shown. However, we need to disable selecting a folder – that’s why we have added 'filesOnly'=>true. The last eval’s parameter is field type. It could be either a checkbox or radio, but since we want to add only one cd cover per album, radio is the thing.

Comment – this is the same field as description field in tl_cds_category.


##Listing child records

At this point, we are able to add new records to the database. Would be nice if we could list them, so they are possible to edit/view/delete and search.

At the end of the tl\_cds.php file, create a new class that extends Backend and contains the listCds function:

```php
class tl_cds extends Backend {

  /**
  * List cds of our collection
  * @param array
  * @return string
  */
  public function listCds($arrRow)
  {
    return '<div>
    <img src=" ' . $arrRow['image'] . '  " style="height:100px; width:100px; float:left; margin-right: 1em;" /><p><strong>' . $arrRow['title'] . '</strong> (' . $arrRow['artist'] . ')</p>' . $arrRow['comment']
    . '</div>' . "\n";
  }

}

?>
```

It is a good convention to name classes same as tables they correspond to. Let’s take a look at the function.

As its first and the only parameter it takes an array that contains data retrieved from the database. The array looks like this:


```php
Array
(
    [id] => 2
    [pid] => 1
    [tstamp] => 1270829730
    [title] => Hellfire Club
    [artist] => Edguy
    [image] => tl_files/Edguy.jpg
    [comment] => <p>In contrast to their previous albums, Hellfire Club owes more to the
sound of Iron Maiden than their biggest influence Helloween, both in
vocals and in music. The first track "Mysteria" opens with the
introduction "Ladies and Gentlemen! Welcome - to the Freak Show!".</p>
)
Array
(
    [id] => 5
    [pid] => 1
    [tstamp] => 1270831831
    [title] => One X
    [artist] => Three Days Grace
    [image] => tl_files/OneX.jpg
    [comment] => <p>One-X is the second album from Three Days Grace, released on June 13,
2006. The album entered the Billboard Top 200 charts at #5 with first
week sales of more than 78,000 and has so far gone to sell over
1,200,000 copies in the US alone.</p>
)
```

Each key corresponds to the field in a database table. I hope both the code and array are clear for you.



