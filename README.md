# Style Guidelines: Markdown

This document contains formatting standards for creating readable, consistent
files using Markdown.

One problem I run into constantly when creating Markdown
files is that I waste an ass-load of time fiddling with how the text looks
before it gets parsed. Then, after I'm finished writing, I waste even more time
adjusting what looks good in my text editor so that it looks good in a
browser or Markdown viewer.

Being a masochist, I of course decided to create a guideline I could follow
which would produce decent looking output without looking stupid in vim.

## Basic conventions for Markdown files

  * Wrap all lines at 80 characters
  * Lines exceeding 80 characters should have, at minimum, three words on
    the following line.
    _(see this list item in raw format for an example.)_
  * Denote **Bold** text using the asterisk format: `**bold text**`.
  * Denote _italic_ text using the underscore format: `_emphasized text_`.
  * Force a linebreak by ending a line with two spaces, no more.

## Headings

  * Header text must use the `atx-style` with no closing `#` character.
  * Include a space between the `#` and the text of the Header.^[1](#1)

    ```
    # Header 1
    ## Header 2
    ### Header 3
    ```

  * Headers spanning more than 80 characters should be re-evaluated.
  * Headers must be preceded and followed by a newline except at the beginning
    of a file.

## Lists

  * **List items** must be indented 2 spaces further than their parent.

    ```
    This is arbitrary text, an unordered list begins on the next line.
      * list item 1
      * list item 2
        * sub-list item
    ```

  * The first level of list items must not be preceded by a newline.
  * All lists must be followed by newlines.

    ```
    This text precedes a list of things.
      * list item 1
      * list item 2
        1. sub-list item 1
        2. sub-list item 2

      * list item 3
      * list item 4

    This is text of any kind that follows a list.
    ```

  * List item lines exceeding 80 characters should, when wrapped, align
    vertically with the beginning of the preceding line's text.

    ```
      * Large, avian creatures, chocobos roughly act as the equivalent of horses,
        being domesticated for use as mounts...
    ```

## Code

  * **Inline code** must use single backticks and must not have spaces between
    the backtick characters and the code.

    ```
    # Bad
    ` .this-is-wrong `

    # Good
    `.this-is-good`
    ```

  * **Fenced code blocks** must be preceded and followed by a newline.
  * When used inside _list items_, **fenced code blocks** must be indented as if
    they were one level deeper that the list item that contains them.

    ```
      * This list item contains a fenced code block
      * Let's show how it might interact with a list.

        ```
        .code-example {
          property: value;
        }
        ```

    There is a newline above this paragraph because it is both the end of a list
    and because it follows a fenced code block.
    ```

## Tables
Like fenced code blocks, tables in Markdown are provided by Markdown Extra which
seems to be pretty widely implemented.

  * Pipe characters must be preceded and followed by spaces for readability.
  * Table column width should be determined by the longest cell in the column.
  * Always format tables so they are readable in pre-processing.

    ```
    # This is completely unreadable, although it is technically valid.
    table header | other table header
    --- | ---
    table data | other table data
    ```

  * Never use preceding or trailing pipes when writing tables.

    ```
    # This wastes our precious 80 character limit.
    | table header | other table header |
    | ------------ | ------------------ |
    | table data   | table data         |
    ```

  * Tables must always be preceded and followed by newlines.

### Table example:

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


## Footnotes
  1. This is enforced locally through redcarpet2's configuration:
     `:space_after_headers`.
     <a name="1"><a>

