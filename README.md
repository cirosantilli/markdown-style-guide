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
  * Denote **Bold** text using the asterisk format: `**bold text**`.
  * Denote _italic_ text using the underscore format: `_emphasized text_`.

## Headings

  * Header text must use the `atx-style` with no closing `#` character.

   ```
   # Header 1
   ## Header 2
   ### Header 3
   ```

  * Headers spanning more than 80 characters should be re-evaluated.
  * Headers must be preceeded and followed by a newline except at the beginning
   of a file.

## Lists

  * **List items** must be indented 2 spaces further than their parent.

   ```
   This is arbitrary text, an unordered list begins on the next line.
     * list item 1
     * list item 2
       * sub-list item
   ```

  * The first level of list items must not be preceeded by a newline.
  * All lists must be followed by newlines.

    ```
    This text preceeds a list of things.
    * list item 1
    * list item 2
      1. sub-list item 1
      2. sub-list item 2

    * list item 3
    * list item 4

    This is text of any kind that follows a list.
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

  * **Fenced code blocks** must be preceeded and followed by a newline.
  * When used inside **list items**, indent **fenced code blocks** as if they
    were one level deeper that the list item that contains them.

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

