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
  <td>Logout</td>
  <td>This type of page automatically logs out the user.</td>
</tr>
<tr>
  <td>403 Access denied</td>
  <td>If a user requests a protected page without permission, a 403 error page
      will be loaded instead. This page must be added <b>on the first level</b>
      inside your website root page.</td>
</tr>
<tr>
  <td>404 Page not found</td>
  <td>If a user requests a non-existent page, a 404 error page will be loaded
      instead. This page must be added <b>on the first level</b> inside your
      website root page.</td>
</tr>
</table>


### Multi-domain mode

Contao supports multiple websites within the site structure and automatically
redirects visitors to a particular website root page depending on its DNS and
language settings. Let us assume that you are running a bilingual corporate
website which uses the domain "www.example.com" and a small private website
which uses the domain "www.personal.example.org". You need three website root
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
  <td>www.personal.example.org</td>
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
  <td>www.example.com</td>
  <td>English</td>
  <td>English corporate website</td>
</tr>
<tr>
  <td>www.example.com</td>
  <td>German</td>
  <td>German corporate website</td>
</tr>
<tr>
  <td>www.example.com</td>
  <td>Spanish</td>
  <td>English corporate website</td>
</tr>
<tr>
  <td>www.personal.example.org</td>
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
allowed to edit the page itself as well as its articles, whereas a user of the
group that owns a page is only allowed to edit articles. Unprivileged users have
no writing permissions at all.

![](images/access-rights.jpg)
