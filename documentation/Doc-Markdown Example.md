# Headings are made with \# signs!
## The more \#'s there are, the smaller the heading

# Fonts

## Italic
Italics are done with \*'s:

```
*This is italic!*
```

*This is italic!*

## Bold

Bold font is done with doub;e \*'s:

```
**This is bold!**
```

**This is bold**

# Lists
Lists are made using dashes (\-) or asterisks (\*). Indentations with tabs indent the list. For example, the code below

```
- Item
- Item
	- Indexed Item

```

Becomes this:

- Item
- Item
	- Indexed Item


# Numbered Lists
Numbered lists are made like so. *(Note: Using 1. for each item is better as Markdown will auto-enumerate the items)*

```
1. Item #1
1. Item #2
	1. Subitem #1
	1. SubItem #2

```

Becomes this:

1. Item #1
1. Item #2
	1. Subitem #1
	1. SubItem #2


# Embedding code
Code can be embedded in two ways, inline or in code blocks. Both involve using the \` character (typically the key left of the 1 key):

Inline code `looks like this`. It doesn't create a new line and appears on the same line of text. For example, this:

```
This is not code, `but this is`
```

Becomes this:

This is not code, `but this is`

Code blocks are formed with a pair of three \` characters. It is useful for showing larger chunks of code. If you browse to the raw version of this Markdown file [here](https://raw.githubusercontent.com/C0atRack/GE02-Collab/main/documentation/Doc-Markdown%20Example.md), you will see I use these code blocks to show before and afters.

# Links

Links take the following form:

```
[link test](https://link.goes/here)
```


# Images

Images can not be directly embedded into Markdown files, at least not easily. You can instead tell Markdown to add an image from a link to the document.
To do so, follow these steps:

1. Upload your image to the [images](https://github.com/C0atRack/GE02-Collab/tree/main/images) folder of the repository:
	![Step #1 of adding images to a Markdown file](https://github.com/C0atRack/GE02-Collab/blob/main/images/Doc%20Embedding%20Images/Embed%20Images%20Step%201.png?raw=true)

1. After uploading the image, browse to the image on Github and open it. It should look something like this:
	![Step #2 of adding images to a Markdown file](https://github.com/C0atRack/GE02-Collab/blob/main/images/Doc%20Embedding%20Images/Embed%20Images%20Step%202.png?raw=true)

1. Copy the link from the URL bar, and then add `?raw=true` to the end. It should end up looking something like this:
	```
	https://github.com/C0atRack/GE02-Collab/blob/main/images/Embed%20Images%20Step%201.png?raw=true

	```
1. Finally, add the image to the Markdown document using the following syntax:
	```
	![Text discription of image](Image link with ?raw=true added)

	Example:
	![Step #1 of adding an images to a Markdown file](https://github.com/C0atRack/GE02-Collab/blob/main/images/Embed%20Images%20Step%201.png?raw=true)
	```
