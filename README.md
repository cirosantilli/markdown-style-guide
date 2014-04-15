Readable, consistent and portable Markdown style.

Considers both the [original specification](http://daringfireball.net/projects/markdown/syntax) and common extensions.

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

    Rationale: `setex` style headers are:

    - harder to write
    - only go up to level 2
    - occupy more screen lines

    Any readability gain they have can be achieved for `atx-style` headers by configuring your editor to syntax highlight `atx-style` headers.

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

Fenced Code Blocks must be preceded and followed by a newline.

# Tables

Like fenced code blocks, tables in Markdown are provided by Markdown Extra which seems to be pretty widely implemented.

- Pipe characters must be preceded and followed by spaces for readability.
- Table column width should be determined by the longest cell in the column.
- Always format tables so they are readable in pre-processing.

    ```
    # This is completely unreadable, although it is technically valid.
    table header | other table header
    --- | ---
    table data | other table data
    ```

- Never use preceding or trailing pipes when writing tables.

    ```
    # This wastes our precious 80 character limit.
    | table header | other table header |
    | ------------ | ------------------ |
    | table data   | table data         |
    ```

- Tables must always be preceded and followed by newlines.

## Table example

This table meets all the criteria:

```
Group                     | Domain          | First Appearance
------------------------- | --------------- | ----------------
ShinRa                    | Mako Reactors   | FFVII
Moogles                   | MogNet          | FFIII
Vana'diel Chocobo Society | Chocobo Raising | FFXI:TOAU
```

A handsome table in pre-processed markdown is also handsome when rendered:

Group                     | Domain          | First Appearance
------------------------- | --------------- | ----------------
ShinRa                    | Mako Reactors   | FFVII
Moogles                   | MogNet          | FFIII
Vana'diel Chocobo Society | Chocobo Raising | FFXI:TOAU
