# Administration area

To access the Contao administration area (back end) simply add `/contao` to the
URL of your Contao website. The back end login is protected against brute force
attacks, so if you enter a wrong password more than three times in a row, your
account will be locked for 5 minutes.


## Listing records

The Contao core engine supports three views: a simple list ("list view"), a list
that is grouped by its parent table ("parent view") and a hierarchical list
("tree view"). These three views can be used to list the records of any table or
related tables.


### List view

The "list view" lists the records of a single table in a particular order. The
results are usually grouped by their first letter.

![](https://raw.github.com/contao/docs/3.0/manual/en/images/list-view.jpg)


### Parent view

The "parent view" lists the records of a child table that are related to a
particular record of a parent table. Parent-child relations are used a lot in
Contao, e.g. for articles and content elements, news archives and news articles
or style sheets and format definitions.

![](https://raw.github.com/contao/docs/3.0/manual/en/images/parent-view.jpg)


### Tree view

The "tree view" lists records and other resources like files and folders that
are organized in a hierarchical structure. Contao supports listing single
hierarchical tables (e.g. the site structure) as well as child tables that
relate to hierarchical parent tables (e.g. articles and pages).

![](https://raw.github.com/contao/docs/3.0/manual/en/images/tree-view.jpg)


### Sorting and filtering data

Contao supports various ways to refine results so you do not lose track even if
a table has several thousands of rows. A lot of listings can be filtered by one
or more fields so they only show the records matching the filter criteria. Most
listings additionally offer a full text search that even supports regular
expressions. To keep the page loading time down to a minimum, Contao only shows
30 records at a time.

![](https://raw.github.com/contao/docs/3.0/manual/en/images/sorting-and-filtering.jpg)


## Editing records

Editing data is one of the central functions of a Content Management System.
Contao offers a lot of professional features that make the editing process as
easy and comfortable as possible. You can revert back to earlier versions of a
record, restore deleted records, move records via clipboard and even edit
multiple records at once. Most of these functions can be accessed using the
navigation icons.


### List view icons

The "list view" being the simplest view only offers the four basic actions:
edit, duplicate, delete and show.

![](https://raw.github.com/contao/docs/3.0/manual/en/images/list-view-icons.jpg)


### Parent view icons

The "parent view" offers two additional navigation icons to control the order of
the records. From version 2.7, the order can also be changed via drag and drop.
To do so, simply click on a record (not a navigation icon) and drag it to its
new position.

![](https://raw.github.com/contao/docs/3.0/manual/en/images/parent-view-icons.jpg)


### Tree view icons

The "tree view" requires additional icons to handle the hierarchical structure.
Besides duplicating a single record, it also supports duplicating a record with
all its sub-records as well as pasting it after or into another record, so you
can create a nested structure.

![](https://raw.github.com/contao/docs/3.0/manual/en/images/tree-view-icons.jpg)


### Restoring prior versions

Contao automatically creates new versions of a record every time you save it. As
soon as there is more than one version, a drop-down menu which allows you to
revert back to a prior version appears at the top of the form. Simply choose a
version and click the "Restore" button.

![](https://raw.github.com/contao/docs/3.0/manual/en/images/versioning.jpg)


### Editing multiple records

The ability to edit more than one record at a time clearly makes Contao stand
out from the variety of Content management systems. Click the "Edit multiple"
button to switch the editing mode, then select one or more records and choose
the fields that you want to modify.

![](https://raw.github.com/contao/docs/3.0/manual/en/images/select-multiple-records.jpg)

![](https://raw.github.com/contao/docs/3.0/manual/en/images/select-fields-to-edit.jpg)

![](https://raw.github.com/contao/docs/3.0/manual/en/images/edit-multiple-records.jpg)


## Keyboard shortcuts

To speed up the workflow when working with Contao, there are several back end
shortcuts which allow you to execute certain commands. You can e.g. trigger the
"save" button at the end of a form by klicking it with your mouse or by using
the keyboard shortcut `[Alt]+[s]`.


### General keyboard shortcuts

<table>
<tr>
  <th>Shortcut</th>
  <th>Button</th>
  <th>Explanation</th>
</tr>
<tr>
  <td><code>[Alt]+[h]</code></td>
  <td><b>H</b>ome</td>
  <td>Go to the home page of the back end.</td>
</tr>
<tr>
  <td><code>[Alt]+[q]</code></td>
  <td><b>Q</b>uit</td>
  <td>Quit the current back end session (log out).</td>
</tr>
<tr>
  <td><code>[Alt]+[t]</code></td>
  <td><b>T</b>op</td>
  <td>Go to the top of the page.</td>
</tr>
<tr>
  <td><code>[Alt]+[b]</code></td>
  <td><b>B</b>ack</td>
  <td>Go back to the previous page.</td>
</tr>
<tr>
  <td><code>[Alt]+[n]</code></td>
  <td><b>N</b>ew record</td>
  <td>Create a new record.</td>
</tr>
<tr>
  <td><code>[Alt]+[e]</code></td>
  <td><b>E</b>dit multiple</td>
  <td>Switch to the "edit multiple" mode.</td>
</tr>
<tr>
  <td><code>[Alt]+[f]</code></td>
  <td><b>F</b>ront end preview</td>
  <td>Open the front end preview in a new browser window.</td>
</tr>
</table>


### Keyboard shortcuts in edit mode

<table>
<tr>
  <th>Shortcut</th>
  <th>Button</th>
  <th>Explanation</th>
</tr>
<tr>
  <td><code>[Alt]+[s]</code></td>
  <td><b>S</b>ave</td>
  <td>Saves the current form.</td>
</tr>
<tr>
  <td><code>[Alt]+[c]</code></td>
  <td>Save and <b>c</b>lose</td>
  <td>Saves the current form and redirects to the previous page.</td>
</tr>
<tr>
  <td><code>[Alt]+[g]</code></td>
  <td>Save and <b>g</b>o back</td>
  <td>Saves the current form and redirects to the parent page, e.g. from a
content element to the article tree.</td>
</tr>
<tr>
  <td><code>[Alt]+[e]</code></td>
  <td>Save and <b>e</b>dit</td>
  <td>Saves the current form and redirects to the child records view, e.g. when
creating style sheets.</td>
</tr>
<tr>
  <td><code>[Alt]+[n]</code></td>
  <td>Save and <b>n</b>ew</td>
  <td>Saves the current form and creates a new record.</td>
</tr>
</table>


### Keyboard shortcuts in "edit multiple" mode

<table>
<tr>
  <th>Shortcut</th>
  <th>Button</th>
  <th>Explanation</th>
</tr>
<tr>
  <td><code>[Alt]+[d]</code></td>
  <td><b>D</b>elete multiple</td>
  <td>Deletes all selected records in "edit multiple" mode.</td>
</tr>
<tr>
  <td><code>[Alt]+[x]</code></td>
  <td>Cut multiple</td>
  <td>Moves all selected records in "edit multiple" mode.</td>
</tr>
<tr>
  <td><code>[Alt]+[c]</code></td>
  <td><b>C</b>opy multiple</td>
  <td>Duplicates all selected records in "edit multiple" mode.</td>
</tr>
<tr>
  <td><code>[Alt]+[v]</code></td>
  <td>Override multiple</td>
  <td>Overrides all selected records in "edit multiple" mode.</td>
</tr>
</table>

The keyboard shortcuts above only work on Windows in this form. Mac users have
to use `[Ctrl]+[⌥ Opt]` instead of the `[Alt]` key together with the keyboard
shortcut. In addition, Firefox on Windows deviates from the standard: you have
to press `[Alt]+[Shift]` and the keyboard shortcut.
