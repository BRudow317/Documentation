# Markdown Documentation

Thanks for visiting [The Markdown Guide](https://www.markdownguide.org)!

This Markdown cheat sheet provides a quick overview of all the Markdown syntax elements. It can’t cover every edge case, so if you need more information about any of these elements, refer to the reference guides for [basic syntax](https://www.markdownguide.org/basic-syntax/) and [extended syntax](https://www.markdownguide.org/extended-syntax/).

## Basic Syntax

These are the elements outlined in John Gruber’s original design document. All Markdown applications support these elements.

### Heading

`# H1`

## H2  

### H3

### Bold

**bold text**  

### Italic

*italicized text*  

### Blockquote

> blockquote

### Ordered List

1. First item
2. Second item
3. Third item

### Unordered List

- First item
- Second item
- Third item

### Code

`code`

### Horizontal Rule

---

### Link

[Markdown Guide](https://www.markdownguide.org)

### Image

![alt text](https://www.markdownguide.org/assets/images/tux.png)

## Extended Syntax

These elements extend the basic syntax by adding additional features. Not all Markdown applications support these elements.

### Table

| Syntax | Description |
| ----------- | ----------- |
| Header | Title |
| Paragraph | Text |

### Fenced Code Block

```json
{
  "firstName": "John",
  "lastName": "Smith",
  "age": 25
}
```

### Footnote

Here's a sentence with a footnote. [^1]

[^1]: This is the footnote.

### Heading ID

### My Great Heading {#custom-id}

### Definition List

term
: definition

### Strikethrough

~~The world is flat.~~

### Task List

- [x] Write the press release
- [ ] Update the website
- [ ] Contact the media

### Emoji

That is so funny! :joy:

(See also [Copying and Pasting Emoji])

### Highlight

I need to highlight these ==very important words==.

### Subscript

H~2~O

### Superscript

X^2^

## Advanced Markdown Guide  

[https://www.markdownguide.org/extended-syntax/#copying-and-pasting-emoji]
[GitHub Flavored Markdown (GFM) https://github.github.com/gfm/]

### Tables Continued  

To add a table, use three or more hyphens (---) to create each column’s header, and use pipes (|) to separate each column. For compatibility, you should also add a pipe on either end of the row.  

| Syntax      | Description |
| ----------- | ----------- |
| Header      | Title       |
| Paragraph   | Text        |

The rendered output looks like this:
Cell widths can vary, as shown below. The rendered output will look the same.  

| Syntax | Description |
| --- | ----------- |
| Header | Title |
| Paragraph | Text |

 Tip: Creating tables with hyphens and pipes can be tedious. To speed up the process, try using the Markdown Tables Generator or AnyWayData Markdown Export. Build a table using the graphical interface, and then copy the generated Markdown-formatted text into your file.

#### Alignment  

You can align text in the columns to the left, right, or center by adding a colon (:) to the left, right, or on both side of the hyphens within the header row.  

| Syntax      | Description | Test Text     |
| :---        |    :----:   |          ---: |
| Header      | Title       | Here's this   |
| Paragraph   | Text        | And more      |

### Formatting Text in Tables  

You can format the text within tables. For example, you can add links, code (words or phrases in backticks (`) only, not code blocks), and emphasis.

You can’t use headings, blockquotes, lists, horizontal rules, images, or most HTML tags.

Tip: You can use HTML to create line breaks and add lists within table cells.
Escaping Pipe Characters in Tables
You can display a pipe (|) character in a table by using its HTML character code (&#124;).

### Footnotes  

Footnotes allow you to add notes and references without cluttering the body of the document. When you create a footnote, a superscript number with a link appears where you added the footnote reference. Readers can click the link to jump to the content of the footnote at the bottom of the page.

To create a footnote reference, add a caret and an identifier inside brackets ([^1]). Identifiers can be numbers or words, but they can’t contain spaces or tabs. Identifiers only correlate the footnote reference with the footnote itself — in the output, footnotes are numbered sequentially.

Add the footnote using another caret and number inside brackets with a colon and text ([^1]: My footnote.). You don’t have to put footnotes at the end of the document. You can put them anywhere except inside other elements like lists, block quotes, and tables.

Here's a simple footnote,[^1]  

Here's a bignote.[^bignote]

[^bignote]: Here's one with multiple paragraphs and code.

    Indent paragraphs to include them in the footnote.

    `{ my code }`

    Add as many paragraphs as you like.

### Heading IDs  

Many Markdown processors support custom IDs for headings — some Markdown processors automatically add them. Adding custom IDs allows you to link directly to headings and modify them with CSS. To add a custom heading ID, enclose the custom ID in curly braces on the same line as the heading.  
For example:

#### My Heading With an ID {myCust-id}

### Linking to Heading IDs  

You can link to headings with custom IDs in the file by creating a standard link with a number sign (#) followed by the custom heading ID. These are commonly referred to as anchor links.
<!-- HTML example: <a href="#heading-ids">Heading IDs</a> -->
Other websites can link to the heading by adding the custom heading ID to the full URL of the webpage.
[Heading IDs](#heading-ids)
(e.g, [Heading IDs](https://www.markdownguide.org/extended-syntax#heading-ids) )  


