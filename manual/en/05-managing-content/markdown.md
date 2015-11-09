## Markdown

Markdown is a lightweight markup language that allows you to format text with
a simple syntax. It has the advantage of being easy to read and write and it 
can be automatically converted to HTML.

You will find some examples of this syntax below:

### Syntax

#### Paragraphs

Paragraphs are separated by line breaks:

    First paragraph

    Second paragraph 


#### Headings

There are six levels of headings:

    # Heading 1
    ## Heading 2
    ### Heading 3
    #### Heading 4
    ##### Heading 5
    ###### Heading 6


#### Strong

To mark important text:

    **strong**
    __strong__

It will be converted to HTML with the following code: `<strong>strong</strong>`


#### Emphasize

To mark text that has stress emphasis:

    *emphasize*
    _emphasize_

It will be converted to HTML with the following code: `<em>emphasize</em>`


#### Code

To mark a piece of computer code:

    `monospaced font`

It will be converted to HTML with the following code: `<code>monospaced font</code>`


##### Block of code

For a block of code, add four spaces before each line.

        monospaced font ...
        ... on several lines


#### Blockquotes

Blockquotes can be created with a right angle bracket placed at the beginning
of the line.

    > This is a blockquote.


#### Line breaks

Add two or more spaces at the end of a line:

    Contao is an accessible Open Source  
    content management system.


#### Links

There are two syntaxes for links: **inline** and **reference**.

An inline link is structured as follows:

    [Contao](https://contao.org/en)

or with an optional title:

    [Contao](https://contao.org/en "Contao's official website")

A reference-style link is structured as follows:

    [Contao's official website][1]
    
    [1]:https://contao.org/en

The reference can be added anywhere in the document.


#### Images

There are also two syntaxes for images as for links.

An inline image is structured as follows:

    ![Alt text](/path/to/img.jpg "Optional title")

A reference-style image is structured as follows:

    ![Alt text][id]

    [id]: /path/to/img.jpg "Optional title"

The reference can be added anywhere in the document.


#### Lists

##### Unordered lists

Unordered lists use asterisks or hyphens:

    * List item  
    * List item  
        * A nested list item
        * A nested list item
    * List item

    - List item  
    - List item  
    - List item


##### Ordered lists

Ordered lists use numbers:

    1. List item  
    2. List item  
    3. List item


### Extended syntax

It is not possible to describe all items with Markdown such as tables or
footnotes for example. That is why there is a project called "Markdown Extra"
that complements the basic language.

You will find some examples of this extended syntax below:


#### Tables

A table can be created like this:

```
First Header | Second Header | Third Header  
------------ | ------------- | ------------  
Content Cell | Content Cell  | Content Cell  
Content Cell | Content Cell  | Content Cell  
```

You can create alignements by adding colons:

```
First Header | Second Header | Third Header  
:----------- | :-----------: | -----------:  
Left         | Center        | Right  
Left         | Center        | Right  
```


#### Footnotes

Footnotes can be created like this:

    That's some text with a footnote.[^1]

    [^1]: And that's the footnote.

The footnote definition can be added anywhere in the document.


### Further information

For a complete documentation about Markdown, please refer to the official
website by following this [link][1].

For a complete documentation about Markdown Extra, please refer to the official
website by following this [link][2].


[1]: http://daringfireball.net/projects/markdown/syntax
[2]: http://michelf.ca/projects/php-markdown/extra
