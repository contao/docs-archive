## Forms

The built-in form generator can be used to create interactive forms that are
sent via e-mail or stored in the Contao database. Uploaded files can be sent as
e-mail attachment or stored in the Contao files directory. The form generator
supports four different data formats:

<table>
<tr>
  <th>Format</th>
  <th>Description</th>
</tr>
<tr>
  <td>Raw data</td>
  <td>The form data will be sent as plain text message with each field in a new
      line.</td>
</tr>
<tr>
  <td>XML file</td>
  <td>The form data will be attached to the e-mail as an XML file.</td>
</tr>
<tr>
  <td>CSV file</td>
  <td>The form data will be attached to the e-mail as a CSV file.</td>
</tr>
<tr>
  <td>E-mail</td>
  <td>Ignores all fields except email, subject, message and cc (carbon copy) and
      sends the form data like it had been sent from a mail client. File uploads
      are allowed.</td>
</tr>
</table>


### Form fields

Similar to content elements, Contao provides a separate element for each type of
form field like text fields, password fields, select menus, file uploads, hidden
fields or submit buttons. Here is an overview of the Contao core form fields:

<table>
<tr>
  <th>Field</th>
  <th>CSS class</th>
  <th>Description</th>
</tr>
<tr>
  <td>Headline</td>
  <td>headline</td>
  <td>A custom field to insert a section headline.</td>
</tr>
<tr>
  <td>Explanation</td>
  <td>explanation</td>
  <td>A custom field to insert an explanation text.</td>
</tr>
<tr>
  <td>HTML code</td>
  <td>-</td>
  <td>A custom field to insert HTML code.</td>
</tr>
<tr>
  <td>Fieldset</td>
  <td>-</td>
  <td>A container for form fields with an optional legend
  (only available for tableless forms).</td>
</tr>
<tr>
  <td>Text field</td>
  <td>text</td>
  <td>A single-line input field for a short or medium text.</td>
</tr>
<tr>
  <td>Password field</td>
  <td>password</td>
  <td>A single-line input field for a password. Contao automatically
      adds a confirmation field.</td>
</tr>
<tr>
  <td>Textarea</td>
  <td>textarea</td>
  <td>A multi-line input field for a medium or long text.</td>
</tr>
<tr>
  <td>Select menu</td>
  <td>select/multiselect</td>
  <td>A single- or multi-line drop-down menu.</td>
</tr>
<tr>
  <td>Radio button menu</td>
  <td>radio</td>
  <td>A list of multiple options from which one can be selected.</td>
</tr>
<tr>
  <td>Checkbox menu</td>
  <td>checkbox</td>
  <td>A list of multiple options from which any can be selected.</td>
</tr>
<tr>
  <td>File upload</td>
  <td>upload</td>
  <td>A single-line input field to upload a local file to the server.</td>
</tr>
<tr>
  <td>Hidden field</td>
  <td>-</td>
  <td>A single-line input field that is not visible in the form.</td>
</tr>
<tr>
  <td>Security question</td>
  <td>captcha</td>
  <td>A simple math question to verify that the form is being
      submitted by a human (CAPTCHA).</td>
</tr>
<tr>
  <td>Submit field</td>
  <td>submit</td>
  <td>A button to submit the form.</td>
</tr>
</table>


### Front end module

The front end module is used to display forms on the website. They can be 
configured with the "Modules" module in the back end and have to be added to an 
article or page layout to actually show up on the website. The form generator 
extension includes one front end module:

<table>
<tr>
  <th>Module</th>
  <th>CSS class</th>
  <th>Description</th>
</tr>
<tr>
  <td>Form</td>
  <td>mod_form</td>
  <td>Adds a form to a page.</td>
</tr>
</table>


### Content element

The content element is used to display forms on the website. They can be 
configured with the "Form" content element in the back end and have to be 
added to an article to actually show up on the website. The form generator 
extension includes one content element:

<table>
<tr>
  <th>Content element</th>
  <th>CSS class</th>
  <th>Description</th>
</tr>
<tr>
  <td>Form</td>
  <td>ce_form</td>
  <td>Includes a form.</td>
</tr>
</table>
