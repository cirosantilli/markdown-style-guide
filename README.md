# Markdown Style Guide

Readable and portable Markdown style guide.

Further design goals:

- easy to write and modify later
- diff friendly
- easy to remember and implement on editors

Considers both the [original specification](http://daringfireball.net/projects/markdown/syntax) and common extensions.

## Why fork Carwin

This guide was forked from [carwin/markdown-styleguide](https://github.com/carwin/markdown-styleguide/tree/9121c77bd177a3ade6713d50ab1228782d7c02a7) because there were many important points in which we disagreed. This guide proposes:

- don't wrap long lines
- lists indented with 4 spaces, not 2
- ordered lists only with `1.`
- italics with `*it*`, not `_it_`
- tables have pipes before and after

The general structure of the guide was kept, but almost every line was modified, and many additions were made.

## File

### File extension

Use `.md`.

Rationale: why not `.mkd` or `.markdown`?

- shorter
- more popular
- does not have important conflicts

### File name

- use lower case letters
- replace punctuation and white space characters by hyphens
- replace consecutive hyphens by a single hyphen
- strip surrounding hyphens

Good:

    file-name.md

Bad, multiple consecutive hyphens:

    file--name.md

Bad, surrounding hyphens:

    -file-name-.md

Rationale: why not underscore or camel case? Hyphens are the most popular URL separator today, and markdown files are most often used in contexts where:

- there are hyphen separated HTML files in the same project, possibly the same directory as the markdown files.
- filenames will be used directly to URLs. E.g.: GitHub blobs.

## General rules

### Consecutive empty lines

*Don't* use 2 or more consecutive empty lines except where they must appear literally such as in code blocks.

Good:

    - list
    - list

    # Header

Good, code block:

    The markup language X requires you to use triple newlines to separate paragraphs:

        p1


        p2

Bad:

    - list
    - list


    # Header

Rationale: multiple empty lines occupy more vertical screen space, and do not significantly improve readability.

### Line wrapping

*Don't* wrap long lines with newlines. Set your editor to wrap them visually instead.

Rationale:

- GitHub breaks the original markdown standard and inserts line breaks at newline characters. Since GitHub is a major markdown player, it is better to be compatible with them.
- diffs look better, since a change to a paragraph shows up as a single diff line.

## Block elements

### Line breaks

Force a line break by ending a line with exactly two spaces.

### Headers

- Use the `atx-style` with no closing `#` character.

    Rationale: `Setex` style headers are:

    - harder to write
    - only go up to level 2
    - occupy more screen lines

    `Setex` headers are more visible, but good visibility can be achieved for `atx-style` headers by configuring your editor to syntax highlight them.
- Include a space between the `#` and the text of the header.
- Headers must be surrounded by one empty line except at the beginning of a file.
- Headers must *not* have spaces preceding the number sign.

Good:

    Before.

    # Header

    After.

Bad:

    Before.
    # Header

    # Header
    After.

    Header
    =======

    # Header #

    #Header

     # Header

#### Top-level header

The *top-level header* is an:

- optional
- `h1` header
- that is the first line of a `.md` file
- and contains the entire file, that is, there are not other `h1` headers in the same file

Top-level headers serve as a title for the entire document.

Projects must be consistent if they use top-level headers or not: files which serve analogous functions must either all have top-level headers or not.

Downsides of top-level headers:

- take up one header level. This means that there are only 5 header levels left, and each new header will have one extra `#`, which looks worse and is harder to write.

- duplicate filename information, which most often can already be seen on a URL. In most cases, the filename can be trivially converted to a top-level, e.g.: `some-filename.md` to `Some filename`.

Advantages of top-level headers:

- more readable than URL's, especially for non-technically inclined users.

If possible, use a technology stack that stores top-level header information outside of the ordinary markdown. For example, in [Jekyll](https://github.com/jekyll/jekyll) projects, top-level header information can be stored as file metadata on the front matter, and used from templates.

#### Header case

- use an upper case letter as the first letter of a header, unless it is a word that always starts with lowercase letters, e.g. computer code.

    Good:

        # Header

    Good, computer code that always starts with lower case:

        # int main

    Bad:

        # header

- the other letters have the same case they would have in the middle of a sentence.

    Good:

        # The header of the example

    Bad:

        # The Header of the Example

    As an exception, [title case](http://en.wikipedia.org/wiki/Title_case#Title_case) may be optionally used for the [top-level header](#top-level-header). Use this exception sparingly, in cases where typographical perfection is important, e.g.: `README` of a project.

    Rationale: why not [Title case](http://en.wikipedia.org/wiki/Title_case#Title_case) for all headers? It requires too much effort to decide if edge-case words should be upper case or not.

#### End of a header

Indicate the end of a header's content that is not followed by a new header by an horizontal rule:

    # Header

    Content

    ---

    Outside header.

### Blockquotes

- Follow the greater than marker by one space.

    Good:

        > a

    Bad:

        >a

    Bad, 2 spaces:

        >  a

- *Don't* use empty lines inside a single block quote.

    Good:

        > a
        >
        > b

    Bad:

        > a

        > b

### Lists

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

    Rationale: same indent as:

    - code blocks, so it is simpler for editors to implement: 1 tab always equals 4 spaces.
    - inner content must have, so inner lists look aligned with inner paragraphs.

        Bad:

            - Outer list.

                Inner paragraph.

              - Inner list. Bad. not aligend.

        It is true that many implementations render the following the same as the above:

            - Outer list.

              Inner paragraph. 2 spaces: not standard.

              - Inner list.

        But the original markdown standard requires 4 spaces for inner paragraphs.

- Either:

    - separate all list items of a list by one empty line to generate `<li><p>`
    - don't separate any of them by empty lines to generate only `<li>`

    Don't mix both, which is unspecified. If you need the mixed case, use raw HTML.

    Good:

        - p

        - p

        - p

    <!-- -->

        - no p
        - no p
        - no p

    Bad, mixed:

        - p

        - no p
        - no p

- Surround lists by one empty line, except for a list without `<p>` inside another.

    Good:

        Before.

        - list
        - list

        After.

    <!-- -->

        - p

        - p

            - no p
            - no p
            - no p

        - p

    <!-- -->

        - p

        - p

            - no p

            - no p

            - no p

        - p

    Good, list without `<p>` inside another:

        - no p
        - no p
            - no p
            - no p
            - no p
        - no p

    Bad:

        Before.
        - list
        - list
        After.

    Bad, list without `<p>` inside list with `<p>` without preceding empty line:

        - no p

        - no p
            - no p
            - no p
            - no p

        - no p

- Avoid multi-paragraph items inside lists without `<p>`, as this adds `<p>` to one element of the list, and some style sheets like GitHub's add an extra vertical space because of that.

    Bad:

        - no p
        - no p
        - no p

            Content
        - no p

    Because this generates:

        <li>no p<li>
        <li>no p<li>
        <li>no p<li>
        <li><p>p. Looks too separated from the item above if compared to the others.</p>
            <p>Content</p>
        <li>p<li>

    Bad for the same reason:

        - no p
        - no p
        - no p

            - p

            - p

        - no p

### Code blocks

Use indented code blocks wherever you can, since they are part of the original standard and fenced code blocks are not.

Code blocks must be surrounded by one empty line.

Indent indented code blocks with 4 spaces.

*Don't* indent fenced code blocks.

### Horizontal rules

*Don't* use horizontal rules except to indicate the [End of a header](#end-of-a-header).

Rationale:

- headers are better section separators since they say what a section is about.
- horizontal rules don't have a generally accepted semantic meaning. This guide gives them one.

Use 3 hyphens without spaces:

    ---

### Tables

Extension.

- Surround tables by one empty line.
- Don't indent tables.
- Surround every line of the table by pipes.
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

### Separate consecutive elements

Separate consecutive:

- lists
- indented code blocks
- blockquotes
- list followed by external code block

with an empty HTML comment `<!-- -->`.

<!-- -->

    - list 1
    - list 1

    <!-- -->

    - list 2
    - list 2

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

<!-- -->

    - list
    - list

    <!-- -->

        code outside list
        code outside list

## Span elements

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

### Bold

Use double asterisk format: `**bold**`.

Rationale: more common and readable than the double underline `__bold__` form.

### Italic

Use single asterisk format: `*italic*`.

Rationale:

- more common and readable than the underscore form
- consistent with the bold format, which also uses asterisks
