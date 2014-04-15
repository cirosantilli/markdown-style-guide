Formatting standards for creating readable, consistent and portable Markdown code.

# Line wrapping

**Don't** wrap long lines. Set your editor to wrap them visualy instead.

Rationale: GitHub breaks the original markdown standard and inserts line breaks at newline characters. Since GitHub is a major markdown player, don't wrap lines for maximum compatibility.

# Line breaks

Force a line break by ending a line with two spaces, no more.

# Inline elements

For all inline elements, **don't** use inner spaces.

Good:

    **bold**
    [link](http://a.com)

Bad:

    ** bold **
    [ link ]( http://a.com )

## Bold

Denote **bold** text using the double asterisk format: `**bold**`.

Rationale: more common and readable than the double underline `__bold__` form.

## Italic

Denote *italic* text using the underscore format: `*italic*`.

Rationale: more common and readable than the underscore form, and consistent with bold.

# Headings

- Header text must use the `atx-style` with no closing `#` character.
- Include a space between the `#` and the text of the header.
- Headers must be preceded and followed by a newline except at the beginning of a file.
- Headers must **not** have spaces preceding the number sign.

Good:

    # Heading

Bad:

    # Heading #

    #Heading

    Content of last heading.
    # Heading
    Content of this heading.

# Lists

- **List items** must be indented 2 spaces further than their parent.

    ```
    This is arbitrary text, an unordered list begins on the next line.
    - list item 1
    - list item 2
      - sub-list item
    ```

- The first level of list items must not be preceded by a newline.
- All lists must be followed by newlines.

    ```
    This text precedes a list of things.
    - list item 1
    - list item 2
        1. sub-list item 1
        2. sub-list item 2

    - list item 3
    - list item 4

    This is text of any kind that follows a list.
    ```

- List item lines exceeding 80 characters should, when wrapped, align vertically with the beginning of the preceding line's text.

    ```
    - Large, avian creatures, chocobos roughly act as the equivalent of
        horses, being domesticated for use as mounts...
    ```

# Code

- **Inline code** must use single backticks and must not have spaces between the backtick characters and the code.

    ```
    # Bad
    ` .this-is-wrong `

    # Good
    `.this-is-good`
    ```

- **Fenced code blocks** must be preceded and followed by a newline.
- When used inside _list items_, **fenced code blocks** must be indented as if they were one level deeper that the list item that contains them.

    ```
    - This list item contains a fenced code block.
    - Let's show how it might interact with a list.

        ```
        .code-example {
          property: value;
        }
        ```

    There is a newline above this paragraph because it is both the end of a
    list and because it follows a fenced code block.
    ```

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

_This table meets all the criteria:_

```
Group                     | Domain          | First Appearance
------------------------- | --------------- | ----------------
ShinRa                    | Mako Reactors   | FFVII
Moogles                   | MogNet          | FFIII
Vana'diel Chocobo Society | Chocobo Raising | FFXI:TOAU
```

_A handsome table in pre-processed markdown is also handsome when rendered:_

Group                     | Domain          | First Appearance
------------------------- | --------------- | ----------------
ShinRa                    | Mako Reactors   | FFVII
Moogles                   | MogNet          | FFIII
Vana'diel Chocobo Society | Chocobo Raising | FFXI:TOAU
