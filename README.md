# Markdown Style Guide

Readable, consistent and portable Markdown style guide.

Considers both the [original specification](http://daringfireball.net/projects/markdown/syntax) and common extensions.

# Why fork Carwin

There were too many important points in which we disagreed with [carwin/markdown-styleguide](https://github.com/carwin/markdown-styleguide/tree/9121c77bd177a3ade6713d50ab1228782d7c02a7). This guide proposes:

- don't wrap long lines
- lists indented with 4 spaces, not 2
- ordered lists only with `1.`
- italics with `*it*`, not `_it_`
- tables have pipes before and after

# File extension

Use `.md`.

Rationale: why not `.mkd` or `.markdown`?

- shorter
- more popular
- does not have important conflicts

# Line breaks

Force a line break by ending a line with exactly two spaces.

# Line wrapping

*Don't* wrap long lines with newlines. Set your editor to wrap them visually instead.

Rationale:

- GitHub breaks the original markdown standard and inserts line breaks at newline characters. Since GitHub is a major markdown player, it is better to be compatible with them.
- diffs look better, since a change to a paragraph shows up as a single diff line.

# Headers

- Use the `atx-style` with no closing `#` character.

    Rationale: `Setex` style headers are:

    - harder to write
    - only go up to level 2
    - occupy more screen lines

    `Setex` headers are more visible, but good visibility can be achieved for `atx-style` headers by configuring your editor to syntax highlight them.
- Include a space between the `#` and the text of the header.
- Headers must be surrounded by an empty line except at the beginning of a file.
- Headers must *not* have spaces preceding the number sign.

Good:

    Before.

    # Heading

    After.

Bad:

    Before.
    # Heading

    # Heading
    After.

    Heading
    =======

    # Heading #

    #Heading

     # Heading

# Blockquotes

- Follow the greater than marker by one space.

    Good:

        > a

    Bad:

        >b

    <!-- -->

        >  b

- *Don't* use empty lines inside a single block quote.

    Good:

        > a
        >
        > b

    Bad:

        > a

        > b

# Lists

- Use the hyphen marker followed by one space for unordered lists.

    Good:

        - a

    Bad:

        -a

    <!-- -->

        -   a

    Rationale:

    - asterisk `*` can be confused with bold or italic markers.
    - plus sign `+` is not popular.

- Only use the marker `1.` for ordered lists.

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

        Diffs will show only the significant line which was modified.

    - content stays aligned without extra effort if the numbers reach 2 digits. E.g.: the following is not aligned:

            9. a
            10. b

- Indented list items and their content by 4 spaces further than their parent. The first level has no indent.

    Good:

        Before.

        - item 1

            Content 1

            - item 11

            Content 1

        - item 2
            - item 21
            - item 22

        After.

- Either:

    - separate all list items of a list by empty lines to generate `<li><p>`
    - don't separate any of them by empty lines to generate only `<li>`

    Don't mix both, which is unspecified.

    Good:

        - a

        - b

        - c

    Good:

        - a
        - b
        - c

    Bad:

        - a

        - b
        - c

    If you absolutely need a mixed case, use raw HTML.

- nested lists. TODO understand this point better

    Good:

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

Use indented code blocks wherever you can, since they are part of the original standard and fenced code blocks are not.

Code blocks must be surrounded by an empty line.

# Tables

Extension.

- Surround by an empty line.
- Don't indent.
- Surround by pipes.
- Align all border pipes vertically.
- Separate header from body by hyphens except at the aligned pipes `|`.
- Pipes `|` must be surrounded by a space, except for:
    - pipes at the header separator, which are surrounded by a hyphen `-`.
    - outer pipes which only get one space or hyphen internally.
- Column width is determined by the longest cell in the column.
- Left align content inside cells. In flavors where header cells determine text alignment, align only the header, and keep the body cells left aligned.

Good table:

    Before.

    | h    |  right align |  center align  |
    |------|--------------|----------------|
    | abc  | def          | ghi            |
    | abc2 | def2         | ghi2           |

    After.

Rationale:

- unaligned tables tables are easier to write, but aligned tables are more readable, and people read code much more often than they edit it.
- preceding pipes make it easier to determine where a table starts and ends. Trailing pipes make it look better because of symmetry.

# Separate consecutive elements

Separate consecutive lists, indented code blocks and blockquotes with an empty HTML comment `<!-- -->`:

    - l1
    - l1

    <!-- -->

    - l2
    - l2

<!-- -->

        code 1
        code 1

    <!-- -->

        code 2
        code 2

<!-- -->

    > blockquote 1
    > blockquote 1

    <!-- -->

    > blockquote 2
    > blockquote 2

# Span elements

*Don't* use inner spaces.

Good:

    **bold**
    `code`
    [link](http://a.com)

Bad:

    ** bold **
    ` code `
    [ link ]( http://a.com )

For inline code in which the space is crucial:

- explain in writing that the spaces must be there
- add something after the space if possible

Good:

    Use the hyphen marker followed by one space `- a`  for unordered lists.

Rationale: most browsers don't render the surrounding spaces nor add them to the clipboard on copy.

## Bold

Use double asterisk format: `**bold**`.

Rationale: more common and readable than the double underline `__bold__` form.

## Italic

Use single asterisk format: `*italic*`.

Rationale:

- more common and readable than the underscore form
- consistent with the bold format, which also uses asterisks
