## Comments

Comments are another form of content that you can manage from the back end. 
Comments must be enabled in the calendar and news archive preferences.


### Front end module

The front end module is used to display comments on the website. They can be 
configured with the "Modules" module in the back end and have to be added to an 
article or page layout to actually show up on the website. The comments 
extension includes one front end module:

<table>
<tr>
  <th>Module</th>
  <th>CSS class</th>
  <th>Description</th>
</tr>
<tr>
  <td>Comments</td>
  <td>mod_comments</td>
  <td>Manage comments or guestbook entries.</td>
</tr>
</table>


### Content element

The content element is used to display comments on the website. They can be 
configured with the "Comments" content element in the back end and have to be 
added to an article to actually show up on the website. The comments extension 
includes one content element:

<table>
<tr>
  <th>Content element</th>
  <th>CSS class</th>
  <th>Description</th>
</tr>
<tr>
  <td>Comments</td>
  <td>ce_comments</td>
  <td>Adds a comment form to the page.</td>
</tr>
</table>


### BBCode

You can allow the front end users to use the [BBCode markup language][7].

Contao supports the following tags:

<table>
<tr>
  <th>BBCode</th>
  <th>Definition</th>
</tr>
<tr>
  <td>[b][/b]</td>
  <td>Replaces the tag with a bolded text.</td>
</tr>
<tr>
  <td>[i][/i]</td>
  <td>Replaces the tag with an italicized text.</td>
</tr>
<tr>
  <td>[u][/u]</td>
  <td>Replaces the tag with an underlined text.</td>
</tr>
<tr>
  <td>[img][/img]</td>
  <td>Replaces the tag with an image (Add an URL between the tags).</td>
</tr>
<tr>
  <td>[code][/code]</td>
  <td>Replaces the tag with a monospaced text.</td>
</tr>
<tr>
  <td>[color=#ff0000][/color]</td>
  <td>Replaces the tag with a colored text.</td>
</tr>
<tr>
  <td>[quote][/quote]</td>
  <td>Replaces the tag with a quoted text.</td>
</tr>
<tr>
  <td>[quote=John]Hello[/quote]</td>
  <td>Replaces the tag with a quoted text and the author name (e.g. John wrote: 
Hello).</td>
</tr>
<tr>
  <td>[url][/url]</td>
  <td>Replaces the tag with a link.</td>
</tr>
<tr>
  <td>[url=http://][/url]</td>
  <td>Replaces the tag with a link (insert the URL as the parameter)</td>
</tr>
<tr>
  <td>[email][/email]</td>
  <td>Replaces the tag with a mailto link.</td>
</tr>
<tr>
  <td>[email=name@example.com][/email]</td>
  <td>Replaces the tag with a mailto link (insert the e-mail address as the 
parameter).</td>
</tr>
</table>


[7]: http://en.wikipedia.org/wiki/BBCode