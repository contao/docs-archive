## Insert tags

Insert tags are wildcards that are replaced with dynamic content when a page is
printed to the screen. They e.g. allow you to show the current date, address a
front end user by his name or include a file. Insert tags can be used almost
anywhere in Contao, even on cached pages.


### Link elements

The following insert tags allow you to link to another page or article using its
ID or alias.

{% raw %}
<table>
<tr>
  <th>Insert tag</th>
  <th>Description</th>
</tr>
<tr>
  <td><code>{{link::*}}</code></td>
  <td>This tag will be replaced with a link to an internal page (replace * with
      the page ID or alias).</td>
</tr>
<tr>
  <td><code>{{link::back}}</code></td>
  <td>This tag will be replaced with a link that points to the last visited page.
      It can also be used as <code>{{link_open::back}}</code>,
      <code>{{link_url::back}}</code> or <code>{{link_title::back}}</code>
      (see below).</td>
</tr>
<tr>
  <td><code>{{link::login}}</code></td>
  <td>This tag will be replaced with a link to the login page of the currently
      logged in front end user (if any).</td>
</tr>
<tr>
  <td><code>{{link_open::*}}</code></td>
  <td>Will be replaced with the opening tag of a link to an internal page:
      <code>{{link_open::12}}Click here{{link_close}}</code>.</td>
</tr>
<tr>
  <td><code>{{link_url::*}}</code></td>
  <td>This tag will be replaced with the URL of an internal page: <code>&lt;a
      href="{{link_url::12}}">Click here&lt;/a&gt;</code>.</td>
</tr>
<tr>
  <td><code>{{link_title::*}}</code></td>
  <td>This tag will be replaced with the title of an internal page: <code>&lt;a
      title="{{link_title::12}}">Click here&lt;/a&gt;</code>.</td>
</tr>
<tr>
  <td><code>{{link_name::*}}</code></td>
  <td>This tag will be replaced with the name of an internal page (replace * with
      the page ID or alias).</td>
</tr>
<tr>
  <td><code>{{link_close}}</code></td>
  <td>Will be replaced with the closing tag of a link to an internal page:
      <code>{{link_open::12}}Click here{{link_close}}</code>.</td>
</tr>
<tr>
  <td><code>{{article::*}}</code></td>
  <td>This tag will be replaced with a link to an article (replace * with the
      article ID or alias).</td>
</tr>
<tr>
  <td><code>{{article_open::*}}</code></td>
  <td>Will be replaced with the opening tag of a link to an article:
      <code>{{article_open::12}}Click here{{link_close}}</code>.</td>
</tr>
<tr>
  <td><code>{{article_url::*}}</code></td>
  <td>This tag will be replaced with the URL of an article: <code>&lt;a
      href="{{article_url::12}}">Click here&lt;/a&gt;</code>.</td>
</tr>
<tr>
  <td><code>{{article_title::*}}</code></td>
  <td>This tag will be replaced with the title of an article: <code>&lt;a
      title="{{article_title::12}}">Click here&lt;/a&gt;</code>.</td>
</tr>
<tr>
  <td><code>{{news::*}}</code></td>
  <td>This tag will be replaced with a link to a news item (replace * with the
      news ID or alias).</td>
</tr>
<tr>
  <td><code>{{news_open::*}}</code></td>
  <td>Will be replaced with the opening tag of a link to a news article:
      <code>{{news_open::12}}Click here{{link_close}}</code>.</td>
</tr>
<tr>
  <td><code>{{news_url::*}}</code></td>
  <td>This tag will be replaced with the URL of a news article: <code>&lt;a
      href="{{news_url::12}}">Click here&lt;/a&gt;</code>.</td>
</tr>
<tr>
  <td><code>{{news_title::*}}</code></td>
  <td>This tag will be replaced with the title of a news article: <code>&lt;a
      title="{{news_title::12}}">Click here&lt;/a&gt;</code>.</td>
</tr>
<tr>
  <td><code>{{news_feed::*}}</code></td>
  <td>This tag will be replaced with the URL of a news feed (replace * with the
      news feed ID).</td>
</tr>
<tr>
  <td><code>{{event::*}}</code></td>
  <td>This tag will be replaced with a link to an event (replace * with the
      event ID or alias).</td>
</tr>
<tr>
  <td><code>{{event_open::*}}</code></td>
  <td>Will be replaced with the opening tag of a link to an event:
      <code>{{event_open::12}}Click here{{link_close}}</code>.</td>
</tr>
<tr>
  <td><code>{{event_url::*}}</code></td>
  <td>This tag will be replaced with the URL of an event: <code>&lt;a
      href="{{event_url::12}}">Click here&lt;/a&gt;</code>.</td>
</tr>
<tr>
  <td><code>{{event_title::*}}</code></td>
  <td>This tag will be replaced with the title of an event: <code>&lt;a
      title="{{event_title::12}}">Click here&lt;/a&gt;</code>.</td>
</tr>
<tr>
  <td><code>{{calendar_feed::*}}</code></td>
  <td>This tag will be replaced with the URL of a calendar feed (replace * with the
      calendar feed ID).</td>
</tr>
<tr>
  <td><code>{{faq::*}}</code></td>
  <td>This tag will be replaced with a link to a frequently asked question
      (replace * with the FAQ ID or alias).</td>
</tr>
<tr>
  <td><code>{{faq_open::*}}</code></td>
  <td>Will be replaced with the opening tag of a link to a question:
      <code>{{faq_open::12}}Click here{{link_close}}</code>.</td>
</tr>
<tr>
  <td><code>{{faq_url::*}}</code></td>
  <td>This tag will be replaced with the URL of a question:
  <code>&lt;a href="{{faq_url::12}}">Click here&lt;/a&gt;</code>.</td>
</tr>
<tr>
  <td><code>{{faq_title::*}}</code></td>
  <td>This tag will be replaced with the title of a question: <code>&lt;a
      title="{{faq_title::12}}">Click here&lt;/a&gt;</code>.</td>
</tr>
</table>
{% endraw %}


### Member properties

The following insert tags allow you to display any property of the currently
logged in member (front end user).

{% raw %}
<table>
<tr>
  <th>Insert tag</th>
  <th>Description</th>
</tr>
<tr>
  <td><code>{{user::firstname}}</code></td>
  <td>This tag will be replaced with the first name of the currently logged in
      member.</td>
</tr>
<tr>
  <td><code>{{user::lastname}}</code></td>
  <td>This tag will be replaced with the last name of the currently logged in
      member.</td>
</tr>
<tr>
  <td><code>{{user::company}}</code></td>
  <td>This tag will be replaced with the company name of the currently logged in
      member.</td>
</tr>
<tr>
  <td><code>{{user::phone}}</code></td>
  <td>This tag will be replaced with the phone number of the currently logged in
      member.</td>
</tr>
<tr>
  <td><code>{{user::mobile}}</code></td>
  <td>This tag will be replaced with the mobile number of the currently logged
      in member.</td>
</tr>
<tr>
  <td><code>{{user::fax}}</code></td>
  <td>This tag will be replaced with the fax number of the currently logged in
      member.</td>
</tr>
<tr>
  <td><code>{{user::email}}</code></td>
  <td>This tag will be replaced with the e-mail address of the currently logged
      in member.</td>
</tr>
<tr>
  <td><code>{{user::website}}</code></td>
  <td>This tag will be replaced with the web address of the currently logged in
      member.</td>
</tr>
<tr>
  <td><code>{{user::street}}</code></td>
  <td>This tag will be replaced with the street name of the currently logged in
      member.</td>
</tr>
<tr>
  <td><code>{{user::postal}}</code></td>
  <td>This tag will be replaced with the postal code of the currently logged in
      member.</td>
</tr>
<tr>
  <td><code>{{user::city}}</code></td>
  <td>This tag will be replaced with the city of the currently logged in
      member.</td>
</tr>
<tr>
  <td><code>{{user::country}}</code></td>
  <td>This tag will be replaced with the country of the currently logged in
      member.</td>
</tr>
<tr>
  <td><code>{{user::username}}</code></td>
  <td>This tag will be replaced with the username of the currently logged in
      member.</td>
</tr>
</table>
{% endraw %}


### Page properties

The following insert tags allow you to display any property of the current page.

{% raw %}
<table>
<tr>
  <th>Insert tag</th>
  <th>Description</th>
</tr>
<tr>
  <td><code>{{page::id}}</code></td>
  <td>This tag will be replaced with the ID of the current page.</td>
</tr>
<tr>
  <td><code>{{page::alias}}</code></td>
  <td>This tag will be replaced with the alias of the current page.</td>
</tr>
<tr>
  <td><code>{{page::title}}</code></td>
  <td>This tag will be replaced with the name of the current page.</td>
</tr>
<tr>
  <td><code>{{page::pageTitle}}</code></td>
  <td>This tag will be replaced with the title of the current page.</td>
</tr>
<tr>
  <td><code>{{page::language}}</code></td>
  <td>This tag will be replaced with the language of the current page.</td>
</tr>
<tr>
  <td><code>{{page::parentAlias}}</code></td>
  <td>This tag will be replaced with the alias of the parent page.</td>
</tr>
<tr>
  <td><code>{{page::parentTitle}}</code></td>
  <td>This tag will be replaced with the name of the parent page.</td>
</tr>
<tr>
  <td><code>{{page::parentPageTitle}}</code></td>
  <td>This tag will be replaced with the title of the parent page.</td>
</tr>
<tr>
  <td><code>{{page::mainAlias}}</code></td>
  <td>This tag will be replaced with the alias of the parent main page.</td>
</tr>
<tr>
  <td><code>{{page::mainTitle}}</code></td>
  <td>This tag will be replaced with the name of the parent main page.</td>
</tr>
<tr>
  <td><code>{{page::mainPageTitle}}</code></td>
  <td>This tag will be replaced with the title of the parent main page.</td>
</tr>
<tr>
  <td><code>{{page::rootTitle}}</code></td>
  <td>This tag will be replaced with the name of the website.</td>
</tr>
<tr>
  <td><code>{{page::rootPageTitle}}</code></td>
  <td>This tag will be replaced with the title of the website.</td>
</tr>
</table>
{% endraw %}


### Environment variables

The following insert tags allow you to display environment variables like the
page name or the request string.

{% raw %}
<table>
<tr>
  <th>Insert tag</th>
  <th>Description</th>
</tr>
<tr>
  <td><code>{{env::host}}</code></td>
  <td>This tag will be replaced with the current host name.</td>
</tr>
<tr>
  <td><code>{{env::url}}</code></td>
  <td>This tag will be replaced with the host name and the protocol.</td>
</tr>
<tr>
  <td><code>{{env::path}}</code></td>
  <td>This tag will be replaced with the current base URL including the path to
      the Contao directory.</td>
</tr>
<tr>
  <td><code>{{env::request}}</code></td>
  <td>This tag will be replaced with the current request string.</td>
</tr>
<tr>
  <td><code>{{env::ip}}</code></td>
  <td>This tag will be replaced with the IP address of the current visitor.</td>
</tr>
<tr>
  <td><code>{{env::referer}}</code></td>
  <td>This tag will be replaced with the URL of the last page visited.</td>
</tr>
<tr>
  <td><code>{{env::files_url}}</code></td>
  <td>This tag will be replaced with the static URL of the files directory.</td>
</tr>
<tr>
  <td><code>{{env::assets_url}}</code></td>
  <td>This tag will be replaced with the static URL of the assets
      directory.</td>
</tr>
</table>
{% endraw %}


### Include elements

The following insert tags allow you to include various resources like articles,
modules or files from the "templates" directory.

{% raw %}
<table>
<tr>
  <th>Insert tag</th>
  <th>Description</th>
</tr>
<tr>
  <td><code>{{insert_article::*}}</code></td>
  <td>This tag will be replaced with the referenced article (replace * with the
      article ID or alias).</td>
</tr>
<tr>
  <td><code>{{insert_content::*}}</code></td>
  <td>This tag will be replaced with the referenced content element (replace *
      with the element ID).</td>
</tr>
<tr>
  <td><code>{{insert_module::*}}</code></td>
  <td>This tag will be replaced with the referenced module (replace * with the
      module ID).</td>
</tr>
<tr>
  <td><code>{{insert_form::*}}</code></td>
  <td>This tag will be replaced with the referenced form (replace * with the
      form ID).</td>
</tr>
<tr>
  <td><code>{{article_teaser::*}}</code></td>
  <td>This tag will be replaced with the teaser of an article (replace * with
      the article ID).</td>
</tr>
<tr>
  <td><code>{{news_teaser::*}}</code></td>
  <td>This tag will be replaced with the teaser of a news item (replace * with
      the news ID).</td>
</tr>
<tr>
  <td><code>{{event_teaser::*}}</code></td>
  <td>This tag will be replaced with the teaser of an event (replace * with the
      event ID).</td>
</tr>
<tr>
  <td><code>{{file::*}}</code></td>
  <td>This tag will be replaced with the content of a .php, .tpl, .xhtml or
      .html5 file from the "templates" directory
      (replace * with the file name). You can also provide arguments:
      <code>{{file::file.php?arg1=val&amp;arg2=val}}</code>.
      You can also retrieve the path of a file from the database with its UUID:
      <code>{{file::6939a448-9b30-11e4-bcba-079af1e9baea}}</code>.</td>
</tr>
</table>
{% endraw %}


### Miscellaneous

The following insert tags allow you to perform miscellaneous tasks like adding
the current date or including lightbox images.

{% raw %}
<table>
<tr>
  <th>Insert tag</th>
  <th>Description</th>
</tr>
<tr>
  <td><code>{{date}}</code></td>
  <td>This tag will be replaced with the current date according to the global
      date format.</td>
</tr>
<tr>
  <td><code>{{date::*}}</code></td>
  <td>This tag will be replaced with the current date according to a custom date
      format.</td>
</tr>
<tr>
  <td><code>{{last_update}}</code></td>
  <td>This tag will be replaced with the date of the last update according to
      the global date format.</td>
</tr>
<tr>
  <td><code>{{last_update::*}}</code></td>
  <td>This tag will be replaced with the date of the last update according to a
      custom date format.</td>
</tr>
<tr>
  <td><code>{{email::*}}</code></td>
  <td>This tag will be replaced with a clickable and encrypted link to an e-mail
      address.</td>
</tr>
<tr>
  <td><code>{{email_open::*}}</code></td>
  <td>This tag will be replaced with a clickable and encrypted link to an e-mail
      address. However, the closing <code>&lt;/a&gt;</code> will not be added.</td>
</tr>
<tr>
  <td><code>{{email_url::*}}</code></td>
  <td>This tag will be replaced by the encrypted e-mail address only.</td>
</tr>
<tr>
  <td><code>{{lang::*}}</code></td>
  <td>This tag can be used to mark foreign words within a text:
      <code>{{lang::fr}}Au revoir{{lang}}</code>. It will be replaced with
      <code>&lt;span lang="fr"&gt;Au revoir&lt;/span&gt;</code> and adds the
      <code>xml:lang="fr"</code> attribute if the doctype is XHTML.</td>
</tr>
<tr>
<td><code>{{post::*}}</code></td>
  <td>This tag will be replaced by a given POST variable.
      It could be used to display fields from a submitted form.</td>
</tr>
<tr>
  <td><code>{{abbr::*}}</code></td>
  <td>Mark abbreviations in a text: <code>{{abbr::World Wide Web}}WWW{{abbr}}</code>.
      It will be replaced with <code>&lt;abbr title="World Wide Web"&gt;WWW&lt;/abbr&gt;</code>.</td>
</tr>
<tr>
  <td><code>{{acronym::*}}</code></td>
  <td>Mark acronyms in a text: <code>{{acronym::Multipurpose Internet Mail
      Extensions}}MIME{{acronym}}</code>. It will be replaced with <code>&lt;acronym
      title="Multipurpose Internet Mail Extensions"&gt;MIME&lt;/acronym&gt;</code>.</td>
</tr>
<tr>
  <td><code>{{ua::*}}</code></td>
  <td>Output properties of the user agent: <code>{{ua::browser}}</code>. It will
      e.g. be replaced with "chrome".</td>
</tr>
<tr>
  <td><code>{{iflng::*}}</code></td>
  <td>This tag will be completely removed if the page language does not match
      the tag language. You can use it to define language-specific labels:
      <code>{{iflng::en}}Your name{{iflng::de}}Ihr Name{{iflng}}</code>.</td>
</tr>
<tr>
  <td><code>{{ifnlng::*}}</code></td>
  <td>This tag will be completely removed if the page language matches the tag
      language. You can use it to define language-specific labels:
      <code>{{ifnlng::de}}Your name{{ifnlng}}{{iflng::de}}Ihr Name{{iflng}}</code>.</td>
</tr>
<tr>
  <td><code>{{image::*}}</code></td>
  <td>This tag will be replaced with the thumbnail of an image (replace *
      with the database ID, UUID or a file system path):
      <code>{{image::58ca4a90-2d30-11e4-8c21-0800200c9a66?width=200&amp;height=150}}</code>.<br>
      <strong>width</strong>: Thumbnail width,<br>
      <strong>height</strong>: Thumbnail height,<br>
      <strong>alt</strong>: Alternative text,<br>
      <strong>class</strong>: CSS class,<br>
      <strong>rel</strong>: rel-attribute (e.g. "lightbox"),<br>
      <strong>mode</strong>: Mode ("proportional", "crop" or "box").</td>
</tr>
<tr>
  <td><code>{{picture::*}}</code></td>
  <td>This tag will be replaced with an image and various image sources depending on your image size
     preferences and if the <code>size</code> parameter is a valid ID (replace * with the database ID, UUID
     or a file system path):
      <code>{{picture::58ca4a90-2d30-11e4-8c21-0800200c9a66?size=1&amp;template=picture_default}}</code>.<br>
      <strong>width</strong>: Thumbnail width,<br>
      <strong>height</strong>: Thumbnail height,<br>
      <strong>alt</strong>: Alternative text,<br>
      <strong>class</strong>: CSS class,<br>
      <strong>rel</strong>: rel-attribute (e.g. "lightbox"),<br>
      <strong>mode</strong>: Mode ("proportional", "crop" or "box"),<br>
      <strong>size</strong>: An image size ID (See Themes -&gt; Image sizes),<br>
      <strong>template</strong>: The default template (picture_default).</td>
</tr>
<tr>
  <td><code>{{label::*}}</code></td>
  <td>This tag will be replaced with a translated label. The first parameter is
      a language file name or an acronym such as <code>CNT</code> (countries) or
      <code>LNG</code> (languages). Examples: <code>{{label::CNT:au}}</code> displays
      "Australia" and <code>{{label::tl_article:title:0}}</code> displays "Title".<br>
      Note that only the first colon is a double colon.</td>
</tr>
<tr>
  <td><code>{{version}}</code></td>
  <td>This tag will be replaced with the current Contao version (e.g.
      3.2.7).</td>
</tr>
<tr>
  <td><code>{{request_token}}</code></td>
  <td>This tag will be replaced with the request token of the current
      session.</td>
</tr>
<tr>
  <td><code>{{toggle_view}}</code></td>
  <td>Adds the link which allows you to switch between mobile and desktop layout.</td>
</tr>
<tr>
  <td><code>{{br}}</code></td>
  <td>This tag will be replaced with the HTML <code>&lt;br&gt;</code> tag
  (line break).</td>
</tr>
</table>
{% endraw %}


### Insert tag flags

Using flags, insert tags can be further processed. For example, the value can be
passed to specific PHP methods. Multiple flags can be applied:

{% raw %}
```
{{ua::browser|uncached}}
{{page::title|decodeEntities|strtoupper}}
```
{% endraw %}

Available flags:

<table>
<tr>
    <th>Flag</th>
    <th>Description</th>
    <th>More information</th>
</tr>
<tr>
    <td><code>uncached</code></td>
    <td>Do not replace insert tag when the page is cached</td>
    <td></td>
</tr>
<tr>
    <td><code>refresh</code></td>
    <td>Do not cache the insert tag, even if it is used multiple times on the
      same page</td>
    <td></td>
</tr>
<tr>
    <td><code>addslashes</code></td>
    <td>Quote a string with slashes</td>
    <td><a target="_blank" href="http://php.net/addslashes">PHP function</a></td>
</tr>
<tr>
    <td><code>stripslashes</code></td>
    <td>Remove the slashes from a quoted string</td>
    <td><a target="_blank" href="http://php.net/stripslashes">PHP function</a></td>
</tr>
<tr>
    <td><code>standardize</code></td>
    <td>Standardize the output (e.g. for a page alias or CSS class)</td>
    <td></td>
</tr>
<tr>
    <td><code>ampersand</code></td>
    <td>Convert ampersands to HTML entities</td>
    <td></td>
</tr>
<tr>
    <td><code>specialchars</code></td>
    <td>Convert special characters to HTML entities</td>
    <td></td>
</tr>
<tr>
    <td><code>nl2br</code></td>
    <td>Inserts HTML line breaks before all newlines in a string</td>
    <td><a target="_blank" href="http://php.net/nl2br">PHP function</a></td>
</tr>
<tr>
    <td><code>nl2br_pre</code></td>
    <td>Same as <code>nl2br</code>, but keeps line breaks in
    <code>&lt;pre&gt;</code> tags</td>
    <td></td>
</tr>
<tr>
    <td><code>strtolower</code></td>
    <td>Make a string lowercase</td>
    <td><a target="_blank" href="http://php.net/strtolower">PHP function</a></td>
</tr>
<tr>
    <td><code>utf8_strtolower</code></td>
    <td>Unicode-aware lowercase conversion</td>
    <td></td>
</tr>
<tr>
    <td><code>strtoupper</code></td>
    <td>Make a string uppercase</td>
    <td><a target="_blank" href="http://php.net/strtoupper">PHP function</a></td>
</tr>
<tr>
    <td><code>utf8_strtoupper</code></td>
    <td>Unicode-aware uppercase conversion</td>
    <td></td>
</tr>
<tr>
    <td><code>ucfirst</code></td>
    <td>Make a string's first character uppercase</td>
    <td><a target="_blank" href="http://php.net/ucfirst">PHP function</a></td>
</tr>
<tr>
    <td><code>lcfirst</code></td>
    <td>Make a string's first character lowercase</td>
    <td><a target="_blank" href="http://php.net/lcfirst">PHP function</a></td>
</tr>
<tr>
    <td><code>ucwords</code></td>
    <td>Uppercase the first character of each word in a string</td>
    <td><a target="_blank" href="http://php.net/ucwords">PHP function</a></td>
</tr>
<tr>
    <td><code>trim</code></td>
    <td>Strip whitespace from the beginning and end of a string</td>
    <td><a target="_blank" href="http://php.net/trim">PHP function</a></td>
</tr>
<tr>
    <td><code>rtrim</code></td>
    <td>Strip whitespace from the end of a string</td>
    <td><a target="_blank" href="http://php.net/rtrim">PHP function</a></td>
</tr>
<tr>
    <td><code>ltrim</code></td>
    <td>Strip whitespace from the beginning of a string</td>
    <td><a target="_blank" href="http://php.net/ltrim">PHP function</a></td>
</tr>
<tr>
    <td><code>utf8_romanize</code></td>
    <td>Romanize the output</td>
    <td></td>
</tr>
<tr>
    <td><code>strrev</code></td>
    <td>Reverse a string</td>
    <td><a target="_blank" href="http://php.net/strrev">PHP function</a></td>
</tr>
<tr>
    <td><code>encodeEmail</code></td>
    <td>Encode email addresses in the output</td>
    <td>see <code>String::encodeEmail</code></td>
</tr>
<tr>
    <td><code>decodeEntities</code></td>
    <td>Decodes HTML entities in the output</td>
    <td>see <code>String::decodeEntities()</code></td>
</tr>
<tr>
    <td><code>number_format</code></td>
    <td>Formats a number (without decimal places)</td>
    <td>see <code>System::getFormattedNumber()</code></td>
</tr>
<tr>
    <td><code>currency_format</code></td>
    <td>Formats a currency (two decimal places)</td>
    <td>see <code>System::getFormattedNumber()</code></td>
</tr>
<tr>
    <td><code>readable_size</code></td>
    <td>Convert file sizes to human readable format</td>
    <td>see <code>System::getReadableSize()</code></td>
</tr>
<tr>
    <td><code>urlencode</code></td>
    <td>URL-encodes strings.</td>
    <td><a target="_blank"
    href="http://php.net/urlencode">PHP function</a></td>
</tr>
<tr>
    <td><code>rawurlencode</code></td>
    <td>URL-encode according to RFC 3986.</td>
    <td><a target="_blank"
    href="http://php.net/rawurlencode">PHP function</a></td>
</tr>
</table>
