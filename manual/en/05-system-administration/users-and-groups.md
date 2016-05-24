## Users and groups

Contao distinguishes between back end users ("users"), who can log into the
administration area, and front end users ("members"), who can log into the
website. Unlike administrators, who have access to all pages and elements by
default ("allow all"), regular users cannot access any resource that has not
been explicitly allowed in their profile or in the profile of one of the groups
they belong to ("deny all").


### Users

Each user can be associated with multiple groups and automatically inherits
their permissions. All permissions are additive, which means that a user
inherits the sum of permissions of all groups he belongs to. If group A grants a
certain right, you cannot revoke it in group B.


#### Pagemounts

Pagemounts define which pages of the site structure a user is allowed to see.
The screenshot below shows the site structure in the view of Helen Lewis.
Although the website contains a lot more pages, she can only see three, because
only the "Courses" page has been mounted in the settings of the "Editors" group.
Note that although Helen Lewis is allowed to see three pages, she can only edit
one of them!

![](images/site-structure-hlewis.jpg)

Being able to see a page does not include the right to edit it (or its
articles). Remember that [page permissions][1] are set in the site structure, so
to enable a page for a user, you have to mount it in his profile and grant
access to it in the site structure.


#### Filemounts

Similar to pagemounts, filemounts define which folders a user is allowed to see.
Below is a screenshot of the file manager in the view of Helen Lewis. She is
only allowed to see the "campus" folder, whereas administrators can see the
whole files directory (`files`).

![](images/file-manager-hlewis.jpg)


#### Allowed fields

As mentioned at the beginning, regular users do not have any default permissions
at all ("deny all"), which also implies that they cannot access any form fields.
Even if they are e.g. allowed to access the news module, the form to create a
new entry will be empty until the administrator enables one or more fields of
the `tl_news` table in the group settings.

![](images/allowed-fields.jpg)


### Members

Managing members (front end users) is a lot easier than managing back end users,
because there are no pagemounts or allowed fields. Member management is mainly
required to control access to protected pages, which is implemented on group
level. Depending on the website configuration, registered members will be able
to see protected pages or access protected downloads that are not available to
guests.


#### Front end preview

As an administrator, you can log in as a particular member and preview the
website with its rights and access restrictions. This action is available in
the members view.

![](images/frontend-preview.jpg)

The front end appears with a preview toolbar and you can switch to another
member at any time by using the field "Front end user". It is also possible to
preview the elements that have not yet been published by the selected member.


[1]: ../03-managing-pages/modules.md#access-control
