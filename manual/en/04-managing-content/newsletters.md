## Newsletters

The newsletter extension allows you to manage and send newsletters and
optionally display them on the website. Unlike articles that are associated with
a particular page, newsletters are organized in channels, which allows you to
easily group or categorize them.


### Recipients

Newsletter subscriptions are normally handled by the respective front end
modules, so you do not have to manage recipients manually. For data privacy
reasons, Contao requires [Double Opt-In][2] subscriptions and stores only the
e-mail address of the subscriber.

![](images/newsletter-recipients.jpg?raw=true)

In case you already have a list of recipients, you can import them into Contao
from a CSV file.


### Personalized newsletters

Insofar as you are sending newsletters to registered members, you can
personalize them with so called "Simple Tokens". Simple tokens are similar to
[insert tags][3] and can be used in both the HTML and the text content of a
newsletter.

```
Dear ##firstname## ##lastname##,

Please check and update your personal data:

Street: ##street##
Postal: ##postal##
City:   ##city##
Phone:  ##phone##
E-mail: ##email##

The Administrator
```

In contrast to insert tags, however, simple tokens do not only allow you to
insert data of the member table `tl_member`, but also to realize simple
if-else statements to e.g. specify the salutation.

```
{if gender=="male"}
Dear Mr ##lastname##,
{elseif gender=="female"}
Dear Mrs ##lastname##,
{else}
Dear Sirs,
{endif}

[newsletter content]

{if phone==""}
Please update your contact details and enter your phone number.
{endif}

The Administrator
```


### Sending newsletters

Especially on shared hosting servers, there are typically limitations regarding
the script execution time and/or the number of e-mails that can be sent per
minute. Contao tries to work around both problems by splitting the sending
process into several cycles to prevent script timeouts and adding a custom
waiting time between each cycle to control the number of e-mails per minute.

![](images/sending-newsletters.jpg?raw=true)


### Front end modules

Front end modules are used to handle subscriptions and to optionally display
newsletters on the website. They can be configured with the "Modules" module in
the back end and have to be added to an article or page layout to actually show
up on the website.

<table>
<tr>
  <th>Module</th>
  <th>CSS class</th>
  <th>Description</th>
</tr>
<tr>
  <td>Subscribe</td>
  <td>mod_subscribe</td>
  <td>Generates a form to subscribe to one or more channels.</td>
</tr>
<tr>
  <td>Unsubscribe</td>
  <td>mod_unsubscribe</td>
  <td>Generates a form to unsubscribe from one or more channels.</td>
</tr>
<tr>
  <td>Newsletter list</td>
  <td>mod_nl_list</td>
  <td>Adds a list of newsletters to the page.</td>
</tr>
<tr>
  <td>Newsletter reader</td>
  <td>mod_nl_reader</td>
  <td>Shows the details of a newsletter.</td>
</tr>
</table>


### Permalinks

Each newsletter has a unique URL (permalink) that can be used to reference it:

```
http://www.example.com/newsletters/items/james-wilson-returns.html
```

The above URL requests the newsletter "james-wilson-returns" via the page
"newsletters". Remember that Contao is a page-based CMS, so if the page
"newsletters" did not exist or if it did not include the newsletter reader
module, the newsletter would not be displayed.


[2]: http://en.wikipedia.org/wiki/Opt_in_e-mail
[3]: 04-managing-content/insert-tags.md#insert-tags