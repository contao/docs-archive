# Contributing

To contribute, please clone the Git repository to your local computer, checkout
the correct branch and edit the `*.md` files. The source files are written in
Markdown and converted into HTML using the GitHub markdown parser, therefore you
can use the [GitHub flavored syntax][1].


## General rules

* Only use ATX style headlines (e.g. `# H1` or `### H3`)
* Use [extended/Github Markdown syntax][tables] to render tables
* Always add two empty lines above each headline
* Always add links at the bottom of the document (e.g. `[Google][1]`)
* Add line breaks after 80 characters in paragraphs


## Code snippets

To highlight code snippets, please specify the language as follows:

    ```php
    // The code goes here
    ```

GitHub can handle this syntax as well but our Markdown parser cannot handle the
GitHub syntax.


## Images

Links to images should be relative to the current document.

    ![](images/synchronization-options.jpg)


## Internal links

Internal links are links that point to another markup file in the same
subdirectory as the file you are editing. Please use the file name and anchor
to create internal links:

    [1]: 03-managing-pages/style-sheets.md#style-sheets

If you are unsure about formatting, just take a look at the existing files.


## Tools / Helpers

Online Markdown Editor: http://jbt.github.io/markdown-editor


[1]: https://help.github.com/articles/github-flavored-markdown
[tables]: https://help.github.com/articles/organizing-information-with-tables/
