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

We are using the GitHub CDN for images, therefore please specify the absolute
URL to any image you upload to the repository:

    ![](https://raw.github.com/contao/docs/3.0/manual/en/images/synchronization-options.jpg)


### Internal links

Internal links are links that point to another markup file in the same
subdirectory as the file you are editing. Please use the file name and anchor
to create internal links:

    [1]: 03-Managing-pages.md#stylesheets

If you are unsure about formatting, just take a look at the existing files.


[1]: https://contao.org/en/manual.html
[2]: http://github.github.com/github-flavored-markdown/
