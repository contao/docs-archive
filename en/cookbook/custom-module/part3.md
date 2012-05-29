#Create a custom Contao module – part three
  
  
![Create a custom TYPOlight module CD Collection](http://blog.qzminski.com/wp-content/uploads/2010/04/introimg.jpg)

In the previous part of the tutorial we have created the Data Container Array for our module. Now when we got our backend section ready, we can create a frontend module that will display our collection on the website. We already have got C, U and D  out of CRUD – now it’s time to develop the Read section.

Before we start, I want to remind you that the frontend section of module usually consists of php files in the module’s root directory and .tpl files in the /templates directory.

The TYPOlight isn’t bulid upon a typical MVC framework, as the controller and model are mixed together. So we can say the php files in the /cd_collection are sort of hybrid. They are used to retreive data from the database, parse it and pass to the templates, which are stored in the /templates directory.


![Controller-template schema](http://blog.qzminski.com/wp-content/uploads/2010/10/controller-template-schema.jpg)

In this tutorial we will develop only a simple cds listing. It isn’t going to be divided into Reader and Listing modules (like News). However, after you finish reading this, you should be able to extend our module into those two parts.

Okay, let’s get to work.


##File structure


First of all, create the two files:

/ModuleCdCollection.php (in the module’s root directory)
/templates/mod_cdcollection.tpl
There is nothing to describe here, so let’s write some code.



##ModuleCdCollection.php


**Note: no working link for "first part" below**

In the first part, we defined in config.php, that our frontend module will use ModuleCdCollection class:

```php
// Front end module
array_insert($GLOBALS['FE_MOD']['miscellaneous'], 0, array
(
 'cd_collection' => 'ModuleCdCollection'
));
```


It is a good convention to name a file the way file_name==class_name. You might know this from various php frameworks.

Now open up the ModuleCdCollection.php file and put the following code:


```php
<?php

class ModuleCdCollection extends Module
{

  protected $strTemplate = 'mod_cdcollection';

  protected function compile()
  {
    //
  }

}

?>
```

As you can see we have created the ModuleCdCollection class that extends Module. The Module class provides two unique functions and one unique variable. The protected variable $strTemplate defines a template file that will be used by module. Notice that we do not include file path, as Contao takes module_root/templates as a default one. I hope you suppose that Contao will look for our template file in path templates/mod_cdcollection.tpl.

The two unique functions for Module are compile() and generate(). Those could be divided into frontend – compile() and backend – generate(). We actually don’t need the generate function as we want to display collection only in the frontend (Contao can display a module in the backend using DCA).

Now, it is time for the most interesting part of module development – the actual coding:

```php
protected function compile()
{
  $intCategory = ($this->Input->get('cat')) ? $this->Input->get('cat') : 1;
  $arrCds = array();

  $objCds = $this->Database->prepare("SELECT * FROM tl_cds WHERE pid=? ORDER BY title")->execute($intCategory);
  $objCategory = $this->Database->prepare("SELECT * FROM tl_cds_category WHERE id=?")->execute($intCategory);
  $objCategories = $this->Database->execute("SELECT id, title FROM tl_cds_category ORDER BY title");

  while ($objCds->next())
  {
    $arrCds[] = array
    (
      'title' => $objCds->title,
      'artist' => $objCds->artist,
      'comment' => $objCds->comment,
      'src' => $objCds->image,
      'alt' => $objCds->title
    );
  }

  while ($objCategories->next())
  {
    $blnSelected = ($objCategories->id == $intCategory) ? true : false;

    $arrCategories[] = array
    (
      'id' => $objCategories->id,
      'title' => $objCategories->title,
      'selected' => $blnSelected
    );
  }

  $this->Template->cds = $arrCds;
  $this->Template->categories = $arrCategories;
  $this->Template->catTitle = $objCategory->title;
  $this->Template->catDescription = $objCategory->description;
}

```



Let’s see what we have done here. Firstly, we retrieve the $_GET['cat'] variable, which will tell our module what category should be displayed. If this variable is not set, automatically display the first added category (id = 1).

Next, we execute three queries to the database: cds list of current category, current category data, full list of categories. The full list of categories will be used to create a dropdown menu, which allows visitor to switch between categories.

In the first while() loop, we get all the cds and put them into array. $objCds->next() makes sure none of the records is omitted.

In the second loop, we do the same thing as before, but with categories. We also flag which of the dropdown menu options is currently active. Usability +1.

Finally, we assign all the data to the template.




##templates/mod_cdcollection.tpl

Now as we got a controller of our module, it is time to create a view. Open the templates/mod_cdcollection.tpl file and put the following code:


```php
<span>Choose the category:</span>

<form action="" method="GET">
<select name="cat">
  <?php foreach($this->categories as $category): ?>
    <option value="<?php echo $category['id']; ?>"<?php if ($category['selected']): ?> selected="selected"<?php endif; ?>><?php echo $category['title']; ?></option>
  <?php endforeach; ?>
</select>
<input type="submit" value="OK" />
</form>

<h3><?php echo $this->catTitle; ?></h3>
<?php echo $this->catDescription; ?>

<table border="0" cellpadding="4">
<?php foreach ($this->cds as $cd): ?>
  <tr>
    <td><img src="<?php echo $cd['src']; ?>" height="100" width="100" alt="<?php echo $cd['alt']; ?>" /></td>
    <td>
      <p><strong><?php echo $cd['title']; ?></strong> (<?php echo $cd['artist']; ?>)</p>
      <?php echo $cd['comment']; ?>
    </td>
  </tr>
<?php endforeach; ?>
</table>
```

Well, this code might look unreadable, so I recommend to paste it into your favourite editor.

Firstly, we have made a form that provides a dropdown menu with the categories. As the option’s value we take category’s id, then we make it selected by default if it’s an active category.

Next, we display the category’s title and description.

We create a table that will holds our cds. Then comes a foreach() loop that goes through our array of cds. I hope this code is clear for you. You could also put this code to check how the array looks like:

```php
<pre><?php print_r($this->cds); ?></pre>
```

Try it out now. It should display something similar to this:


![Final image](http://blog.qzminski.com/wp-content/uploads/2010/10/final.jpg)




##Labels

Although our module is working, we should make it more user friendly in the backend. What I mean is changing the e.g. {title_legend} to “CD title”.

Create a new directory “en” in the /languages folder. Then create three files called tl_cds.php, tl_cds_category.php and modules.php.

Notice that the naming convention is the same as in /dca folder.

Okay, open up the languages/en/tl_cds_category.php and put the following code:



```php
<?php

/**
 * Fields
 */
$GLOBALS['TL_LANG']['tl_cds_category']['title']       = array('Title', 'Please enter the title of the category.'); // 1
$GLOBALS['TL_LANG']['tl_cds_category']['description'] = array('Description', 'Please enter the description of the category.'); // 2

/**
 * Legends
 */
$GLOBALS['TL_LANG']['tl_cds_category']['title_legend'] = 'Title and description'; // 3

/**
 * Buttons
 */
$GLOBALS['TL_LANG']['tl_cds_category']['new']    = array('New category', 'Create a new category'); // 4
$GLOBALS['TL_LANG']['tl_cds_category']['show']   = array('Category details', 'Show details of category ID %s'); // 5
$GLOBALS['TL_LANG']['tl_cds_category']['edit']   = array('Edit category', 'Edit category ID %s'); // 6
$GLOBALS['TL_LANG']['tl_cds_category']['copy']   = array('Copy category', 'Duplicate category ID %s'); // 7
$GLOBALS['TL_LANG']['tl_cds_category']['delete'] = array('Delete category', 'Delete category ID %s'); // 8

?>
```


I have prepared a screenshot to explain better what line describes what:

![Category labels](http://blog.qzminski.com/wp-content/uploads/2010/10/labels_backend.jpg)


Now a little explanation where to get the labels’ variables from.

**Fields** are taken directly from the dca file:


```php

// Fields
  'fields' => array
  (
    'title' => array
    (
      'label'             => &$GLOBALS['TL_LANG']['tl_cds_category']['title'],
      'inputType'         => 'text',
      'search'            => true,
      'eval'              => array('mandatory'=>true, 'maxlength'=>64)
    ),
// ...
```


Field’s label is an array, which first element contains the field’s title, while the second one contains the description (also known as explanation) of the field.

**Legends** are taken from the “palettes” array:


```php
// Palettes
'palettes' => array
(
  'default'                     => '{title_legend},title,description'
),
```

**Buttons** are taken from “opreations” array. However, notice that there is one additional label:



```php
$GLOBALS['TL_LANG']['tl_cds_category']['new']    = array('New category', 'Create a new category');
```

This button is not defined in the dca array, and is visible unless the table config’s array has got the “closed” property set to true 'closed' => true.

That’s all of the labels theory for now. Let’s fill the tl_cds.php file:



```php
<?php

/**
 * Fields
 */
$GLOBALS['TL_LANG']['tl_cds']['title']   = array('CD Title', 'Please enter the title of the CD.');
$GLOBALS['TL_LANG']['tl_cds']['artist']  = array('Artist', 'Please enter the author of the CD.');
$GLOBALS['TL_LANG']['tl_cds']['image']   = array('Cover image', 'Please choose the CD cover image.');
$GLOBALS['TL_LANG']['tl_cds']['comment'] = array('Comment', 'Please enter your comment about CD.');

/**
 * Legends
 */
$GLOBALS['TL_LANG']['tl_cds']['title_legend']   = 'Title and artist';
$GLOBALS['TL_LANG']['tl_cds']['image_legend']   = 'CD Cover';
$GLOBALS['TL_LANG']['tl_cds']['comment_legend'] = 'Comment';

/**
 * Buttons
 */
$GLOBALS['TL_LANG']['tl_cds']['new']    = array('New CD', 'Create a new CD');
$GLOBALS['TL_LANG']['tl_cds']['show']   = array('CD details', 'Show details of CD ID %s');
$GLOBALS['TL_LANG']['tl_cds']['edit']   = array('Edit CD', 'Edit CD ID %s');
$GLOBALS['TL_LANG']['tl_cds']['copy']   = array('Copy CD', 'Duplicate CD ID %s');
$GLOBALS['TL_LANG']['tl_cds']['delete'] = array('Delete CD', 'Delete CD ID %s');

?>
```

The above code is very similar to the previous one. I think it doesn’t need any additional explanation.

Okay, we already got the “internal” labels ready. Now we should create few other labels that are displayed in miscellaneous sections of Contao.

Open the languages/en/modules.php file and put the following content:


```php
<?php

/**
 * Back end modules
 */
$GLOBALS['TL_LANG']['MOD']['cd_collection'] = array('CD Collection', 'Manage your CD collection.');

/**
 * Front end modules
 */
$GLOBALS['TL_LANG']['FMD']['cd_collection'] = array('CD Collection list', 'adds a list of cds to your page.');

?>
```

Instead of explaining what they affect, I will simply show you on the image:



![Labels from modules.php](http://blog.qzminski.com/wp-content/uploads/2010/10/labels_modules.jpg)


##Securing files

As the last point, I want to show you how to simply secure our files that they can’t be accessed directly. This method is used in (almost) all php files in Contao.

Now open up all the php files of our module and replace the <?php  tag with:


```php
<?php if (!defined('TL_ROOT')) die('You can not access this file directly!');
```



##Final notes

Congratulations! You have just developed your own Contao module! I hope none part of this tutorial was difficult for you, as I explained everything as much as I could. Thank you very much for your attention. Till next time.



##Download files

Download all files included in this tutorial – [cd_collection.zip](http://blog.qzminski.com/wp-content/uploads/2010/10/cd_collection.zip) (~ 12kB).



