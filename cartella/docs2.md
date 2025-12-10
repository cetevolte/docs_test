**version**: 1.040: 13 Oct 2024

This is a raw conversion from a Google Doc (For verification purposes: use HTML headings and Reckless mode options for both Markdown and HTML conversion, no other options).

DEV VERIFICATION: Docs to Markdown (GD2md-html)

This page both demonstrates and tests the features of [Docs to Markdown](https://workspace.google.com/marketplace/app/docs_to_markdown/700168918607) conversion from a Google Doc to a simple Markdown or HTML file. 

**Note**: Not all Markdown renderers support all Markdown features. For example github Markdown does not support a table of contents ([TOC]), footnotes, or definition lists. Also, some Markdown environments strip heading IDs and replace them with their own generated IDs. You’ll have to do some manual adjustments, depending on your target environment.

[[TOC]]

**Note**: If you find any bugs, please file them at [https://github.com/evbacher/gd2md-html/issues](https://github.com/evbacher/gd2md-html/issues). Thanks for helping to make Docs to Markdown better!

# Headings

Docs to Markdown converts headings to the corresponding heading level in Markdown or HTML. If you use a lot of Heading 1 headings in your Doc, but you want to adhere to the HTML convention of only a single H1 heading per page, you can use the Demote headings option.

# Heading IDs

If you generate a table of contents (with blue links) in your Doc, Docs to Markdown will create IDs for each heading—this also allows proper conversion of intra-doc links. If your Markdown environment does not handle heading attributes, you can choose the HTML headings/IDs option. See [Links](?tab=t.0#heading=h.nfsbs9qkqpz7) for some internal link tests. A link to a different heading with the same words, [Heading IDs](?tab=t.0#heading=h.enui06tom4vc), should go to that heading.

# Blank headings

From here to END BLANK HEADINGS are headings that are empty or contain only whitespace.

#   	

## **  		  **

###   		   

######    			   

END BLANK HEADINGS

## Basic paragraphs

This is a paragraph. (NOTE:  Docs to Markdown supports footnotes!) (Docs to Markdown also supports footnotes) A sentence with some embedded code. Docs to Markdown changes "smart quotes" to straight quotes in code to guard against cut-and-paste errors.

## Basic font styling

This is *italic* text. This is **bold** text. This is **_bold and italic_** text.

## Font attribute runs including extra whitespace at the ends

For example a** bold run with some whitespace **on either end. Here’s an* italic run *with added whitespace. And a strikethrough run with additional whitespace. And some code with added whitespace. And some underline with added whitespace. Links [http://www.google.com](http://www.google.com). Link with no space:[http://www.google.com](http://www.google.com).

Some *italic***_text_***alternating***_with_***bold***_italic_** but no spaces between font changes.

## Mixed font spans

Some regular text, *followed by an italic span* **_with some embedded bold_** *text*. (Note: this may still be a problem, depending on how it’s formatted in the Google Doc. Like this: Some regular text, *followed by an italic span ***_with some embedded bold_*** text*.

Some more regular text. Some strikethrough text here. 

Some strikethrough text at the end of the paragraph.

Followed by some regular text.

## Mixed code spans

Docs to Markdown uses Markdown for most inline code, but it will also handle mixed code spans like this: $ ls -l **_filename_**, by using HTML markup.

## Lists

Docs to Markdown supports numbered lists, ordered lists, and definition lists.

### Numbered lists (ordered lists)

Here is a numbered list:

1. Item one.

2. Item two.

### Unordered lists

And here is a bullet list:

* A list item without any punctuation

* A list item with an embedded command: ps aux | grep conky | grep -v grep | awk '{print $2}' | xargs kill

* Some mixed-font code: ls -l **_filename_**. Followed by some normal text.

### Another ordered list

1. First item

2. Second item

3. Third item

### A nested ordered list

1. First item

2. Second item (this item has nested items below it)

    1. First nested item

    2. Second nested item

3. Third item

### Lists with code blocks

You can have a code block within a list item, as long as you indent the code  (in the Doc) the same amount as the list: 

* A text item, followed by a code block that's indented and should be part of this item:

// A comment.

some code;

  callFunction();

* Another item.

    * A nested list item with a command:

$ cat file | grep dog | wc

### Lists with embedded paragraphs

Note: Works for Markdown, still a known issue for HTML.

* A bullet list with an additional paragraph:

This is another paragraph (Note that GitHub renders an indented HTML paragraph under a list item as a code block! markdownlivepreview.com renders it properly as a paragraph.)

This is a new paragraph, but also part of this list item. It should be indented

* Another item.

    * A nested item.

This is a new paragraph within the nested item.

// Some code after a nested paragraph.

callSomeFunction();

* Another list item.

* And another.

    * Nested

A paragraph within a list item.

        * Nested

A paragraph within a list item.

    * Reducing the nesting level.

* First-level list item.

A regular paragraph.

### Checkbox lists

1. Task 1 (completed)

2. Task 2

### Definition lists

Because Google Docs does not have a definition list element, Docs to Markdown uses a simple but explicit syntax that is similar to the kramdown syntax for definition lists:

?term on a line by itself (starting with a question mark)

:Definition preceded by a colon.

### Definition list examples

**Note**: Github-flavored Markdown does not support Markdown definition-list syntax. You can select a definition list in a Google Doc and convert it to HTML if you’re using it in a GFM page.

? term

: Definition here.

?term1

?term2

: First paragraph of definition.

: Second paragraph of definition.

renders as:

?   term

: Definition here.

?term1

?term2

: First paragraph of definition.

: Second paragraph of definition.

?   A term that has some **_crazy formatting_** and characters (not recommended)//.

: Definition of crazy term.

But a definition term cannot be empty:

?

: Empty term above causes an error here.

## Code blocks

A code block (note that by default, Docs to Markdown does *not* add language descriptors to code blocks, but see [Code Blocks with lang specification](?tab=t.0#heading=h.syco34spl29h)):

package main

import "fmt"

func main() {

	fmt.Println("Hello, 世界")

}

A single-cell table also becomes a code block:

<table>
 <tr>
  <td>#include<stdio.h>
main()
{
    printf("Hello World");
}</td>
 </tr>
</table>


If you have "smart quotes" in regular text, they should be preserved. But if you have any smart quotes in “code” or code blocks, Docs to Markdown removes them during the conversion:

func main() {

	fmt.Println("Why would you do this?")

}

## Code blocks with lang specification

Docs to Markdown supports an optional lang specification on the first line of the code sample (in the Doc source). The syntax is: lang: *langspec*

For example, here is a code block that specifies lang:c on the first line:

lang:c

#include<stdio.h>
main()
{
    printf("Hello World");
}

This also works in single-cell tables: here is a single-cell table that specifies lang: java on the first line:

<table>
 <tr>
  <td>lang: java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World");
    }
}</td>
 </tr>
</table>


## Code blocks with HTML

Code with some embedded HTML tags that should be displayed, not interpreted:

lang:html

This is <code>some code</code>

and some <strong>bold text</strong>.

A single-cell table with some HTML inside:

<table>
 <tr>
  <td>This is some code
     We want to handle as code block;

Preserve whitespace, <code>HTML tags</code>, etc.
Make a fenced code block in Markdown,
        pre in HTML.</td>
 </tr>
</table>


## Tables

Docs to Markdown generates HTML tables.

A table:

<table>
 <tr>
  <td>Some text.</td>
  <td>some code
  var i = 0;</td>
 </tr>
 <tr>
  <td>More text.</td>
  <td>A list:
mozzarella cheese</td>
 </tr>
</table>


You can also merge columns and rows in tables:

<table>
 <tr>
  <td>This row merges the first three columns.
one</td>
  <td></td>
  <td></td>
  <td>four</td>
 </tr>
 <tr>
  <td>one</td>
  <td>two</td>
  <td>These two rows are merged

three</td>
  <td>four</td>
 </tr>
 <tr>
  <td>one</td>
  <td>two</td>
  <td></td>
  <td>four</td>
 </tr>
</table>


## Internal links

Some internal links to headings in this doc (note that you need to generate a TOC with blue links in this doc for these intra-doc links to work):

* [Heading IDs](?tab=t.0#heading=h.w9shf4dpypi9)

* [Code blocks](?tab=t.0#heading=h.yhpbe0sh5kep)

## Heading IDs

This is a duplicate heading (on purpose). An internal link to this heading should come here, not to [Heading IDs](?tab=t.0#heading=h.w9shf4dpypi9) up top.

## Links

Some regular URL links:

* [http://www.google.com/](http://www.google.com/)

* [https://fivethirtyeight.com/](https://fivethirtyeight.com/)

Some links with titles:

* [Jason Kottke's blog](http://kottke.org/)

* [Bean Road](https://beanroad.blogspot.com/)

## Images

A plain image:

![image alt text](image_0.png)

Note that the image link will be broken until you store the image file on your server and adjust the path and width if necessary.

Alternatively, you can use a Drawing to display an image. Here's an example where we've pasted the image into a Drawing and referenced it after converting the doc:

![image alt text](image_1.jpg)

Tip: You can limit the width of an image in Markdown by adding (for example) {width="75%"} after the link markup (if your Markdown engine supports such syntax). For HTML, just add a width="75%" attribute to the img tag.

## Drawings

Google Docs does not provide an API for accessing the data in a Google Drawing. If you have an inline drawing, Docs to Markdown will warn and provide an alert in the converted output:

You can display Google Drawings (and images in Drawings) by reference. See [Google Drawings by reference](https://github.com/evbacher/gd2md-html/wiki/Google-Drawings-by-reference) for details.

Here's an example where we've referred to a drawing by reference (after converting):

Tip: For any drawing that you display by reference, be sure to change the permissions to make it viewable by anyone with the link.

## Equations

If you insert an equation using Google Docs, Docs to Markdown will warn and insert an alert message in the output. However, if your target publishing platform supports LaTeX equations, you can use LaTeX syntax directly.

A Google Docs equation:

A LaTeX equation:

$$e^{i\pi } = -1$$

renders as:

$$e^{i\pi } = -1$$

## Right-to-left text

A few Arabic words هذه فقرة تجريبية inside an English paragraph:

They should appear as in this RTL paragraph:

هذه فقرة تجريبية 

## Soft line-breaks

lineBreak
This line contains a shift-enter soft line-break here
This bit is after the line break.

This is a line with some bold text interrupted by a soft line **break (shift-enter) here
Followed by more bold** and some more regular text.

This paragraph has an explicit line-break (Enter) here.

And this is a separate paragraph.

## Special characters (FEATURE REQUEST)

FEATURE REQUEST: Angle bracket escapes:

* Angle brackets: If you put angle brackets in your text: < or >, we don't want that to render as an HTML tag. So, we use &amp;lt; for the opening bracket by default. However, if you select the Render HTML tags option, the opening < will not be replaced.

* Test: it seems that loose angle brackets < and > do not behave like HTML tags. But when there is no whitespace: <some text>, they do behave like HTML tags. To change that behavior, we’ll need to (by default) escape the opening angle bracket and turn it into &amp;lt;. 

* But if you really want an angle bracket while using the default setting (to insert a few HTML tags), you can escape it: \<tag>, \<div class=’someclass’>. Not escaped: <tag>. Also not escaped: <p>This is an HTML paragraph.<p>

* Escaped: \<p>This is an HTML paragraph.\<p>

Note that we need to replace the opening <, even if it occurs at the beginning of a line, like this:

<br><img src="img1.png"/><br>

Let’s also check for one at the end of a line, though that would be unusual: <

Apparently, it's not a problem in code blocks (the tags are never rendered):

This is a code block with some <html> tags.

This is some regular text.

<table>
 <tr>
  <td>This is a single-cell table code block with some <html> tags.</td>
 </tr>
</table>


This is some more regular text.

## Subscript and superscript processing

A sentence with subscript and superscript and some more regular text and [a link to Google](http://www.google.com).

And more **bold** and mixed**_ _****bold****_ italic _**code and some more text. Some *italic text*.

Another paragraph with **some bold text**.

SUPA subscript or superscript at the beginning or end of a paragraph should not break things:SUB

1. A numbered list following a terminal subscript.

2. Another list item.

## Horizontal rules

This is a horizontal rule:

* * *


This is a regular paragraph.

## Blank Lines

Line 1

Line 2

## Centered/Right aligned text

Handle centered, right-aligned text for Markdown/HTML (in progress). Note that GitHub flavored Markdown does not honor horizontal alignment styling.

Right-aligned paragraph.

Left-aligned paragraph.

Center-aligned paragraph.

Left-aligned paragraph.

### Center-aligned Heading

Regular paragraph.

## Bugs

* Current open bugs: [https://github.com/evbacher/gd2md-html/issues](https://github.com/evbacher/gd2md-html/issues) 

* New bug or feature request: [https://github.com/evbacher/gd2md-html/issues/new](https://github.com/evbacher/gd2md-html/issues/new). Thanks for helping to make Docs to Markdown better!

## End

This document ends with this regular paragraph (though footnotes may follow).
