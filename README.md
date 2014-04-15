# Markdown Style Guide

Readable, consistent and portable Markdown style guide.

Considers both the [original specification](http://daringfireball.net/projects/markdown/syntax) and common extensions.

# File extension

Use `.md`.

Rationale: why not `mkd` or `markdown`? `md` is:

- shorter
- the most common one
- does not have important conflicts

# Line wrapping

*Don't* wrap long lines. Set your editor to wrap them visually instead.

Rationale: GitHub breaks the original markdown standard and inserts line breaks at newline characters. Since GitHub is a major markdown player, don't wrap lines for maximum compatibility.

# Line breaks

Force a line break by ending a line with two spaces, no more.

# Inline elements

For all inline elements, *don't* use inner spaces.

Good:

    **bold**
    `code`
    [link](http://a.com)

Bad:

    ** bold **
    ` code `
    [ link ]( http://a.com )

## Bold

Denote **bold** text using the double asterisk format: `**bold**`.

Rationale: more common and readable than the double underline `__bold__` form.

## Italic

Denote *italic* text using the underscore format: `*italic*`.

Rationale: more common and readable than the underscore form, and consistent with bold.

# Headings

- Header text must use the `atx-style` with no closing `#` character.

    Rationale: `Setex` style headers are:

    - harder to write
    - only go up to level 2
    - occupy more screen lines

    `Setex` headers are more visible, but this equal visibility can be achieved for `atx-style` headers by configuring your editor to syntax highlight them.

- Include a space between the `#` and the text of the header.
- Headers must be preceded and followed by a newline except at the beginning of a file.
- Headers must *not* have spaces preceding the number sign.

Good:

    # Heading

Bad:

    Heading
    =======

    # Heading #

    #Heading

     # Heading

    Content of last heading.
    # Heading
    Content of this heading.

# Lists

- For unordered lists, only use the hyphen `-` marker, followed by one space:

    Rationale:

    - asterisk `*` can be confused with bold or italic markers.
    - plus sign `+` is very rare.

- For ordered lists, use only the marker `1.`.

    Good:

        1. a
        1. b
        1. c

    Bad:

        1. a
        2. b
        3. c

    Rationale:

    - if you want to change a list item in the middle of the list, you don't have to modify all items that follow it.
    - content stays aligned without extra effort if the numbers reach 2 digits. E.g.: the following is not aligned:

            9. a
            10. b

- Indented list items and their content by 4 spaces further than their parent. The first level has no indent.

    Good:

        External paragraph.

        - item 1

            Content 1

            - item 11

            Content 1

        - item 2
            - item 21
            - item 22

- Either separate all list items of a list by newlines, or don't separate any of them, but never mix both, which is unspecified what happens in mixed cases. If you absolutely need a mixed case, use raw HTML.

    TODO understand this point better. The standard is underspecified here.

    Good:

        External paragraph.

        - par

            - nopar
            - nopar
            - nopar
                - par

                - par

                - par

        - par

        - par

    Bad:

        External paragraph.

        - par

        - par

            - nopar
            - nopar

            - BAD: mixed tyle. Should not have newline.

                - par

                - par
                - BAD: mixed style. Should have newline.
        - BAD: mixed style. Should have newline.

# Code Blocks

Prefer indented code blocks wherever you can use them, since they are part of the original standard.

Fenced code blocks (extension) must be preceded and followed by a newline.

# Tables

Extension.

- Separate header from body by hyphens.
- Always use preceding and trailing pipes.
- Align all pipes of a table border vertically.
- Left align content, except for the header lines in flavors where they determine text alignment. The body of explicitly aligned columns must still be left aligned. 
- Column width is determined by the longest cell in the column.
- Must always be preceded and followed by newlines.

Good table:

    | h    |  right align |  center align  |
    |------|--------------|----------------|
    | abc  | def          | ghi            |
    | abc2 | def2         | ghi2           |

Rationale: unaligned tables tables are much easier to write, but the readability gain of alignment is so large that we have decided to use aligned tables always. People read code much more often than they edit it.
