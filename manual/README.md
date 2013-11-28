# Contao Manual

This is the official manual for users and developers used on [contao.org][1].


## Contributing

To contribute, please clone the Git repository to your local computer, checkout
the correct branch and edit the `*.md` files. The source files are written in
Markdown and converted into HTML using the GitHub markdown parser, therefore you
can use the [GitHub flavored syntax][2].


### General rules

* Only use ATX style headlines (e.g. `# H1` or `### H3`)
* Always add two empty lines above each headline
* Always add links at the bottom of the document (e.g. `[Google][1]`)
* Use plain HTML markup to render tables
* Add line breaks after 80 characters in paragraphs


### Code snippets

To highlight code snippets, please specify the language as follows:

    ``` {.php}
    // The code goes here
    ```

GitHub can handle this syntax as well but our Markdown parser cannot handle the
GitHub syntax.


### Images

Links to images should be relative to the current document.
To make them work on GitHub, please add `raw=true` as a parameter:

    ![](images/synchronization-options.jpg?raw=true)


### Internal links

Internal links are links that point to another markup file in the same
subdirectory as the file you are editing. Please use the file name and anchor
to create internal links:

    [1]: 03-Managing-pages.md#stylesheets

If you are unsure about formatting, just take a look at the existing files.

### Tools / Helpers
Online Markdown Editor: http://jbt.github.io/markdown-editor

## Licensing

The Contao manual is licensed under a [Creative Commons Attribution 3.0
License][3] license (CC BY-NC-SA 3.0). If you want to redistribute a modified or
unmodified version of the manual, you can do so under the license terms.

If you contribute to the manual, e.g. by creating pull requests, you grant us
full usage rights of any content you create or upload. You also ensure that your
content does not violate any third-party rights.

We are not claiming exclusive usage rights, therefore you are free to use your
contributed content (e.g. texts or images) in any other project as well.


[1]: https://contao.org/en/manual.html
[2]: http://github.github.com/github-flavored-markdown/
[3]: http://creativecommons.org/licenses/by-nc-sa/3.0/
