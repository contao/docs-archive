# Managing pages

The following chapters explain how to manage pages in Contao. Since Contao is a
page-based content management system, pages and the site structure are the
central elements of your website and any content that is not associated with a
page can never be viewed.


## Components

Understanding how pages, articles, content elements and modules relate to each
other is the key to learning Contao. As mentioned before, the site structure is
the central element of your website. Visitors of your website always request
pages and not articles like in a node-based CMS.

![](https://raw.github.com/contao/docs/3.1/manual/en/images/components.jpg)

The diagram shows that articles and layouts are the two most important page
elements. Whereas articles store the content of a page, the page layout defines
how it is displayed on the website. Contao layouts are CSS-based and of course
do not use layout tables. The following chapters explain how to create style
sheets and modules, how to combine them in a page layout and how to create pages
that are using it.


## Themes

Although the theme manager is a new feature in version 2.9, it is actually just
an enhanced interface to something that has been part of Contao ever since. A
website design typically consists of style sheets, front end modules, page
layouts, files and templates, which you can manage in the Contao back end. The
theme manager does not change this approach at all, it just adds an option to
export and import those resources.


### Themes versus front end templates

The main difference between [themes][1] and front end templates is that a front
end template contains a fully preconfigured example website, including an
example site structure, articles, content elements and even users and groups. A
theme, in contrast, contains only the actual website design and can therefore be
imported without losing any existing data.

![](https://raw.github.com/contao/docs/3.1/manual/en/images/theme-manager.jpg)


### Theme components

A theme is a group of [style sheets][2], [front end modules][3] and [page
layouts][4], which are all stored in the database and automatically recognized
by the theme exporter. You will learn more about those elements in the following
chapters. A theme typically also includes images and other files from the files
directory and optional custom templates from the templates directory. However,
those resources are not automatically linked with the theme and therefore have
to be added in the theme configuration to be included in the theme export.

![](https://raw.github.com/contao/docs/3.1/manual/en/images/theme-settings.jpg)


### Theme export and import

To export a theme, simply click on the export button and download the .cto file
to your local computer. Although .cto is a proprietary file extension for Contao
themes, the file is actually a ZIP archive that can be extracted with every
program that handles .zip files. To reimport the theme, upload the .cto file to
your Contao installation, open the theme manager and click on "Theme import".
You can import multiple themes at once. After the import has been completed, you
can assign the page layout(s) of the new theme in the site structure.


## Style sheets

Accessible websites should always be styled using CSS, that is why Contao
includes a "style sheets" module which allows you to manage format definitions
in the back end. To reference the various Contao elements,you need to know their
class names. [Content element classes][5] start with "ce_" (e.g. "ce_text") and
[module classes][3] with "mod_" (e.g. "mod_search"). If you are not sure, simply
look into the page source.

![](https://raw.github.com/contao/docs/3.1/manual/en/images/style-sheet.jpg)

Every style sheet can be limited to one or more media types and/or to a
particular Internet Explorer version, in case you need to fix one of its
numerous bugs. Pay attention to the order of the format definitions, because
later commands override earlier ones.

``` {.css}
/* Set the general value first */
.mod_search {
    margin:24px;
}

/* Then override it for IE7 */
*:first-child+html .mod_search {
    margin:18px;
}
```

If the order was reversed, the general value would override the IE-specific
margin.


## Modules

Front end modules allow you to add almost any kind of functionality to your
website. The Contao core includes modules to generate various navigation menus,
handle user registration and authentication, search the website, import RSS
feeds and many more. To create a module, log into the back end and choose
"Themes" -> "Front end modules" in the navigation menu.

<table>
<tr>
  <th>Module</th>
  <th>CSS class</th>
  <th>Description</th>
</tr>
<tr>
  <td>Navigation menu</td>
  <td>mod_navigation</td>
  <td>Generates a navigation menu from the site structure.</td>
</tr>
<tr>
  <td>Custom navigation</td>
  <td>mod_customnav</td>
  <td>Generates a custom navigation menu.</td>
</tr>
<tr>
  <td>Breadcrumb navigation</td>
  <td>mod_breadcrumb</td>
  <td>Generates a breadcrumb navigation menu.</td>
</tr>
<tr>
  <td>Quick navigation</td>
  <td>mod_quicknav</td>
  <td>Generates a drop-down menu from the site structure.</td>
</tr>
<tr>
  <td>Quick link</td>
  <td>mod_quicklink</td>
  <td>Generates a custom drop-down menu.</td>
</tr>
<tr>
  <td>Book navigation</td>
  <td>mod_booknav</td>
  <td>Generates a book navigation menu.</td>
</tr>
<tr>
  <td>Article navigation</td>
  <td>mod_article_nav</td>
  <td>Generates a pagination menu to navigate articles.</td>
</tr>
<tr>
  <td>Sitemap</td>
  <td>mod_sitemap</td>
  <td>Generates a list of all pages in the site structure.</td>
</tr>
<tr>
  <td>Login form</td>
  <td>mod_login</td>
  <td>Generates a login form.</td>
</tr>
<tr>
  <td>Automatic logout</td>
  <td>-</td>
  <td>Automatically logs out a user.</td>
</tr>
<tr>
  <td>Personal data</td>
  <td>mod_personalData</td>
  <td>Generates a form to edit a user's personal data.</td>
</tr>
<tr>
  <td>Registration</td>
  <td>mod_registration</td>
  <td>Generates a user registration form.</td>
</tr>
<tr>
  <td>Lost password</td>
  <td>mod_password</td>
  <td>Generates a form to request a new password.</td>
</tr>
<tr>
  <td>Close account</td>
  <td>mod_closeAccount</td>
  <td>Generates a form to delete a member account.</td>
</tr>
<tr>
  <td>Newslist</td>
  <td>mod_newslist</td>
  <td>Adds a list of news items to the page.</td>
</tr>
<tr>
  <td>Newsreader</td>
  <td>mod_newsreader</td>
  <td>Shows the details of a news item.</td>
</tr>
<tr>
  <td>News archive</td>
  <td>mod_newsarchive</td>
  <td>Adds a news archive to the page.</td>
</tr>
<tr>
  <td>News archive menu</td>
  <td>mod_newsmenu</td>
  <td>Generates a navigation menu to browse the news archive.</td>
</tr>
<tr>
  <td>Calendar</td>
  <td>mod_calendar</td>
  <td>Adds a calendar to the page.</td>
</tr>
<tr>
  <td>Event reader</td>
  <td>mod_eventreader</td>
  <td>Shows the details of an event.</td>
</tr>
<tr>
  <td>Event list</td>
  <td>mod_eventlist</td>
  <td>Adds a list of events to the page.</td>
</tr>
<tr>
  <td>Event list menu</td>
  <td>mod_eventmenu</td>
  <td>Generates a navigation menu to browse the event list.</td>
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
<tr>
  <td>FAQ list</td>
  <td>mod_faqlist</td>
  <td>Adds a list of frequently asked questions to the page.</td>
</tr>
<tr>
  <td>FAQ reader</td>
  <td>mod_faqreader</td>
  <td>Shows the answer to a frequently asked question.</td>
</tr>
<tr>
  <td>FAQ page</td>
  <td>mod_faqpage</td>
  <td>Shows the FAQ list and FAQ reader on the same page.</td>
</tr>
<tr>
  <td>Form</td>
  <td>mod_form</td>
  <td>Adds a form to a page.</td>
</tr>
<tr>
  <td>Search engine</td>
  <td>mod_search</td>
  <td>Adds a search form to a page.</td>
</tr>
<tr>
  <td>Comments</td>
  <td>mod_comments</td>
  <td>Manage comments or guestbook entries.</td>
</tr>
<tr>
  <td>Listing</td>
  <td>mod_listing</td>
  <td>Lists the records of a table.</td>
</tr>
<tr>
  <td>Flash movie</td>
  <td>mod_flash</td>
  <td>Embeds a Flash movie into a page.</td>
</tr>
<tr>
  <td>Article list</td>
  <td>mod_article_list</td>
  <td>Generates a list of articles of a column.</td>
</tr>
<tr>
  <td>Random image</td>
  <td>mod_random_image</td>
  <td>Adds a random image to a page.</td>
</tr>
<tr>
  <td>Custom HTML</td>
  <td>-</td>
  <td>Allows you to add custom HTML code.</td>
</tr>
<tr>
  <td>RSS reader</td>
  <td>mod_rss_reader</td>
  <td>Adds an RSS feed to a page.</td>
</tr>
</table>


### Access control

Each front end module can be protected so only guests or members of a particular
group can see it on the website.

![](https://raw.github.com/contao/docs/3.1/manual/en/images/protected-module.jpg)


## Page layouts

Page layouts determine the basic page setup, e.g. the number of columns or the
overall width, and they define which front end modules are shown in which
columns. They also allow you to include style sheets, to link to RSS or Atom
feeds, to associate a Google Analytics ID and to add arbitrary JavaScript code
that is required to control interactive elements and plugins. The Contao CSS
framework automatically divides the browser window into several layout sections
and shows the modules that have been assigned to them one below the other.

![](https://raw.github.com/contao/docs/3.1/manual/en/images/front-end-structure.jpg)

![](https://raw.github.com/contao/docs/3.1/manual/en/images/front-end-modules.jpg)

That implies that by the time you create a page layout, you have to have created
all style sheets and front end modules that you want to include in it. Therefore
it is recommended to create resources in the following order:

* Create the necessary front end modules
* Create the necessary style sheets
* Optionally create news archives or calendars
* Create a new page layout and combine the components


## Page types

The page type determines whether a page shows content, forwards to another page
or defines the starting point of a new website within the page tree. Contao
supports 6 different page types which are explained below.

<table>
<tr>
  <th>Page type</th>
  <th>Description</th>
</tr>
<tr>
  <td>Regular page</td>
  <td>A regular page contains articles and content elements. It behaves like a
      static HTML page.</td>
</tr>
<tr>
  <td>External redirect</td>
  <td>This type of page automatically redirects visitors to an external website.
      It works like a hyperlink.</td>
</tr>
<tr>
  <td>Internal redirect</td>
  <td>This type of page automatically forwards visitors to another page within
      the site structure.</td>
</tr>
<tr>
  <td>Website root</td>
  <td>This type of page marks the starting point of a new website within the
      site structure.</td>
</tr>
<tr>
  <td>403 Access denied</td>
  <td>If a user requests a protected page without permission, a 403 error page
      will be loaded instead.</td>
</tr>
<tr>
  <td>404 Page not found</td>
  <td>If a user requests a non-existent page, a 404 error page will be loaded
      instead.</td>
</tr>
</table>


### Multi-domain mode

Contao supports multiple websites within the site structure and automatically
redirects visitors to a particular website root page depending on its DNS and
language settings. Let us assume that you are running a bilingual corporate
website which uses the domain "www.company.com" and a small private website
which uses the domain "www.personal-website.com". You need three website root
pages for that:

<table>
<tr>
  <th>Type</th>
  <th>DNS</th>
  <th>Language code</th>
  <th>Fallback language</th>
</tr>
<tr>
  <td>German corporate website</td>
  <td>none</td>
  <td>de</td>
  <td>no</td>
</tr>
<tr>
  <td>English corporate website</td>
  <td>none</td>
  <td>en</td>
  <td>yes</td>
</tr>
<tr>
  <td>Personal website</td>
  <td>personal-website.com</td>
  <td>de</td>
  <td>yes</td>
</tr>
</table>

The following table shows to which page a visitor will be redirected depending
on the domain and his browser language.

<table>
<tr>
  <th>Domain</th>
  <th>Browser language</th>
  <th>Redirect target</th>
</tr>
<tr>
  <td>www.company.com</td>
  <td>English</td>
  <td>English corporate website</td>
</tr>
<tr>
  <td>www.company.com</td>
  <td>German</td>
  <td>German corporate website</td>
</tr>
<tr>
  <td>www.company.com</td>
  <td>Spanish</td>
  <td>English corporate website</td>
</tr>
<tr>
  <td>www.personal-website.com</td>
  <td>irrelevant</td>
  <td>Personal website</td>
</tr>
</table>

Note that if we had not set the "language fallback" option, the personal website
would only be available for German speaking users!


### Access rights

Access rights determine what back end users are allowed to do with a page and
its articles. It has nothing to do with protected pages that can only be
accessed by certain front end users! Similar to the Unix file permission system,
there are three permission levels:

* Access as the owner of a page
* Access as a member of the group that owns the page
* Access as an unprivileged user


Each level can have different permissions. By default, the owner of a page is
allowed to edit the page itself as well as its articles, whereas a member of the
group that owns a page is only allowed to edit articles. Unprivileged users have
no writing permissions at all.

![](https://raw.github.com/contao/docs/3.1/manual/en/images/access-rights.jpg)


[1]: https://contao.org/en/contao-themes-and-templates.html
[2]: 03-Managing-pages.md#style-sheets
[3]: 03-Managing-pages.md#modules
[4]: 03-Managing-pages.md#page-layouts
[5]: 04-Managing-content.md#articles
