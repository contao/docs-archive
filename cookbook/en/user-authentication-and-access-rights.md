# User authentication and access rights

The following chapter describes how to check the authentication status and
rights of a user in an extension.

> #### info:: Note
> Contao distinguishes between back end users ("users"), who can log into the
> administration area, and front end users ("members"), who can log into the
> website. For more information about this subject, please refer to the
[user and groups][1] section of the manual.


## Back end

Contao performs the user authentication automatically. The code for the back end
is located in the file `contao/main.php`:


```php
public function __construct()
{
    $this->import('BackendUser', 'User');
    parent::__construct();

    $this->User->authenticate();
}
```


### Accessing the user object in the back end

The user object is a singleton object and can be accessed like this:

```php
$objUser = BackendUser::getInstance();
echo $objUser->username;
```

Because access to the back end is not possible without authentication, one can
assume that there is always an authenticated user in the back end.


### Check the admin status

An administrator can be identified with the flag `isAdmin`:

```php
if ($objUser->isAdmin) {
    // everything is allowed
}
```


### Checking the user groups

A user usually belongs to one or more user groups. Checking if a user belongs
to a group can be accomplished with the method `isMemberOf()`:

```php
if ($objUser->isMemberOf(3)) {
    // the user belongs to the group with the ID 3
}
```

An array with the IDs of all user groups of which the user is member of, can be
retrieved through the field `groups`:

```php
print_r($objUser->groups);
```


### Checking the access rights

There are two major methods for checking the access rights:

* `hasAccess()`: checks whether a user has a particular right
* `isAllowed()`: checks whether a particular action is allowed on a page


#### The method `hasAccess()`

The method `hasAccess()` allows to check, for example, whether a user has
access to a back end module:

```php
if ($objUser->hasAccess('news', 'modules')) {
    // the user is allowed to access the news module
}
```

It can also check whether the access is allowed to a specific news archive:

```php
if ($objUser->hasAccess(2, 'news')) {
    // the user is allowed to access the news archive with the ID 2
}
```

Or whether the user has the right to create a new news feed:

```php
if ($objUser->hasAccess('create', 'newsfeedp')) {
    // the user has the right to create new news feed
}
```

And it can also check the pagemounts or the filemounts permissions of a user:

```php
if ($objUser->hasAccess(11, 'pagemounts')) {
    // the user is allowed to access the page with ID 11
}
```

At last, it can check the access of each field of each table with the
method `hasAccess()`:

```php
if ($objUser->hasAccess('tl_faq::published', 'alexf')) {
    // the user is allowed to access the field "published" from the table "tl_faq"
}
```

Der zweite Parameter der Methode `hasAccess()` bezieht sich auf das Feld in der
Tabelle `tl_user` bzw. `tl_user_group`, in dem die jeweilige Berechtigung
gespeichert ist. Zum Beispiel fragt "modules" das Feld `tl_user.modules` bzw.
`tl_user_group.modules` ab.


#### The method `isAllowed()`

The method `isAllowed()` can check which rights the user has on a specific page
(access rights).

```php
$objPage = PageModel::findByPk(6);

if ($objUser->isAllowed(1, $objPage->row())) {
    // the user is allowed to edit the page with ID 6
}

if ($objUser->isAllowed(2, $objPage->row())) {
    // the user can change the hierarchy of the page with ID 6
}

if ($objUser->isAllowed(3, $objPage->row())) {
    // the user can delete the page with ID 6
}

if ($objUser->isAllowed(4, $objPage->row())) {
    // the user is allowed to edit the article of the page with ID 6
}

if ($objUser->isAllowed(5, $objPage->row())) {
    // the user can change the hierarchy of the article of the page with ID 6
}

if ($objUser->isAllowed(6, $objPage->row())) {
    // the user can delete the article of the page with ID 6
}
```


## Front end

Also in the front end the authentication is performed automatically, but we can
not assume that there is always an authenticated member.


### Accessing the user object in the front end

The user object is a singleton object and can be accessed like this:

```php
$objUser = FrontendUser::getInstance();
echo $objUser->username;
```

The login status can be called through the constant `FE_USER_LOGGED_IN`:

```php
if (FE_USER_LOGGED_IN === true) {
    $objUser = FrontendUser::getInstance();
    // there is an authenticated front end user
} else {
    // there is no authenticated front end user
}
```


### Check member groups

In the front end the access check is performed through the membership in
a group, which can be called thanks to the method `isMemberOf()`:

```php
if ($objUser->isMemberOf(3)) {
    // the user belongs to the group with the ID 3
}
```

An array with the IDs of all member groups, whose a member belongs, can be
called through the field `groups`:

```php
print_r($objUser->groups);
```


[1]: https://docs.contao.org/books/manual/3.5/en/05-system-administration/users-and-groups.html
