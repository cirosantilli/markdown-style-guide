---
title: Markdown Style Guide
layout: default
---

Readable and portable Markdown style guide.

Considers both the [original specification](http://daringfireball.net/projects/markdown/syntax) and common extensions.

<ol data-toc></ol>

# Design goals

- readable
- portable: produces the same output, or good output, across multiple implementations
- easy to write and modify later
- diff friendly
- easy to remember and implement on editors

# Notable users

- [GitLab](https://github.com/gitlabhq/gitlabhq/blob/master/CONTRIBUTING.md#style-guides)

Do you use this style guide? Add your name to [our wiki](https://github.com/cirosantilli/markdown-styleguide/wiki/Users).

Are you notable? Send a pull request.

If you are a notable user:

- you can opt to be contacted before any major changes happen to the standard. Please inform this on the pull request that adds you to the notable list.

- your vote on decisions will have much greater weight

You are more likely to be notable if your project:

- uses Markdown heavily. E.g.: Markdown engines, text editors, lots of markdown documentation, etc.

- is popular. Any popularity measure will be taken into account, e.g. GitHub stars, Google Rank, etc. 2K+ GitHub stars makes for a very strong case.

# Why fork Carwin

This guide was forked from [carwin/markdown-styleguide](https://github.com/carwin/markdown-styleguide/tree/9121c77bd177a3ade6713d50ab1228782d7c02a7) because there were many important points in which we disagreed. This guide proposes:

- don't wrap long lines
- lists indented with 4 spaces, not 2
- ordered lists only with `1.`
- italics with `*it*`, not `_it_`
- tables have pipes before and after

The general structure of the guide was kept, but almost every line was modified, and many additions were made.

# File

## File extension

Use `.md`.

Rationale: why not `.mkd` or `.markdown`?

- shorter
- more popular
- does not have important conflicts

## File name

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

# General rules

## Space

*Don't* use 2 or more consecutive empty lines, that is, more than two consecutive newline characters, except where they must appear literally such as in code blocks.

End files with a newline character, and *don't* leave empty lines at the end of the file.

*Don't* use trailing whitespace unless it has a function such as indicating a line break.

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

## Line wrapping

*Don't* wrap long lines with newlines. Set your editor to wrap them visually instead.

Rationale:

- GitHub breaks the original markdown standard and inserts line breaks at newline characters. Since GitHub is a major markdown player, it is better to be compatible with them.
- diffs look better, since a change to a paragraph shows up as a single diff line.

# Block elements

## Line breaks

Avoid line breaks, as they don't have generally accepted semantic meaning.

In the rare case you absolutely need them, end a lines with exactly two spaces.

## Headers

-   Use the `atx-style` with no closing `#` character.

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

### Top-level header

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

Prefer to start headers of files without a top-level header at level `h1`.

### Header case

-   Use an upper case letter as the first letter of a header, unless it is a word that always starts with lowercase letters, e.g. computer code.

    Good:

        # Header

    Good, computer code that always starts with lower case:

        # int main

    Bad:

        # header

-   The other letters have the same case they would have in the middle of a sentence.

    Good:

        # The header of the example

    Bad:

        # The Header of the Example

    As an exception, [title case](http://en.wikipedia.org/wiki/Title_case#Title_case) may be optionally used for the [top-level header](#top-level-header). Use this exception sparingly, in cases where typographical perfection is important, e.g.: `README` of a project.

    Rationale: why not [Title case](http://en.wikipedia.org/wiki/Title_case#Title_case) for all headers? It requires too much effort to decide if edge-case words should be upper case or not.

### End of a header

Indicate the end of a header's content that is not followed by a new header by an horizontal rule:

    # Header

    Content

    ---

    Outside header.

## Blockquotes

-   Follow the greater than marker by one space.

    Good:

        > a

    Bad:

        >a

    Bad, 2 spaces:

        >  a

-   *Don't* use empty lines inside a single block quote.

    Good:

        > a
        >
        > b

    Bad:

        > a

        > b

## Lists

### Marker

#### Unordered

Use the hyphen marker.

Good:

    - a
    - b

Bad:

    * a
    * b

<!-- -->

    + a
    + b

Rationale:

- asterisk `*` can be confused with bold or italic markers.
- plus sign `+` is not popular.

#### Ordered

Only use the marker `1.` for ordered lists.

Good:

    1. a
    1. b
    1. c

Bad:

    1. a
    2. b
    3. c

Rationale:

-   If you want to change a list item in the middle of the list, you don't have to modify all items that follow it.

    Diffs will show only the significant line which was modified.

-   Content stays aligned without extra effort if the numbers reach 2 digits. E.g.: the following is not aligned:

        9. a
        10. b

### Spaces after marker

- If the content of every item of the list is one line long, use a **1** space.
- Otherwise, use **3** spaces.

Good:

    - a
    - b

<!-- -->

    -   a

        par

    -   b

            code

    -   c

Bad, single line content only:

    -   a
    -   b

Bad, multi-line content with a single space

    - a

        par

#### Rationale: why not always single space?

Because important engines such as Marked and Kramdown indent relative to the last character, and are currently reluctant to even add options that allow to change that behavior, see: <https://github.com/chjj/marked/issues/227>, <https://github.com/gettalong/kramdown/issues/121>.

Therefore they compile:

    - a

            code

As:

    <pre><code>  code

with **2 extra spaces**, Instead of:

    <pre><code>code

This goes against our interpretation of the Original markdown documentation:

> To put a code block within a list item, the code block needs to be indented twice — 8 spaces or two tabs

and also from the actual behavior of the original markdown.

On the other hand, all major engines compile:

    -   a

            code

without the two extra spaces, so we chose that for greater compatibility.

This divergence probably happened because all the examples of the original markdown documentation are of the above form.

Most major engines however don't add the two extra spaces.

### Indented lists

-   Indented list items and their content by 4 spaces further than their parent. The first level has no indent.

    Good:

        Before.

        -   item 1

            Content 1

            - item 11

            Content 1

        -   item 2

            - item 21
            - item 22

        After.

    Rationale: same indent as:

    -   code blocks, so it is simpler for editors to implement: 1 tab always equals 4 spaces.
    -   inner content must have, so inner lists look aligned with inner paragraphs.

        Bad:

            -   Outer list.

                Inner paragraph.

              - Inner list. Bad. not aligend.

        It is true that many implementations render the following the same as the above:

            - Outer list.

              Inner paragraph. 2 spaces: not standard.

              - Inner list.

        But the original markdown standard requires 4 spaces for inner paragraphs.

### Newlines for separation

-   Either:

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

-   Surround lists by one empty line, except for a list without `<p>` inside another.

    Good:

        Before.

        - list
        - list

        After.

    <!-- -->

        -   p

        -   p

            - no p
            - no p
            - no p

        -   p

    <!-- -->

        -   p

        -   p

            - no p

            - no p

            - no p

        -   p

    Good, list without `<p>` inside another:

        -   no p
        -   no p
            - no p
            - no p
            - no p
        -   no p

    Bad:

        Before.
        - list
        - list
        After.

    Bad, list without `<p>` inside list with `<p>` without preceding empty line:

        -   no p

        -   no p
            - no p
            - no p
            - no p

        -   no p

-   Avoid multi-paragraph items inside lists without `<p>`, as this adds `<p>` to one element of the list, and some style sheets like GitHub's add an extra vertical space because of that.

    Bad:

        -   no p
        -   no p
        -   no p

            Content
        -   no p

    Because this generates:

        <li>no p<li>
        <li>no p<li>
        <li>no p<li>
        <li><p>p. Looks too separated from the item above if compared to the others.</p>
            <p>Content</p>
        <li>p<li>

    Bad for the same reason:

        -   no p
        -   no p
        -   no p

            - p

            - p

        -   no p

## Code blocks

Use indented code blocks wherever you can, since they are part of the original standard and fenced code blocks are not.

Code blocks must be surrounded by one empty line.

Indent indented code blocks with 4 spaces.

*Don't* indent fenced code blocks.

## Horizontal rules

*Don't* use horizontal rules except to indicate the [End of a header](#end-of-a-header).

Rationale:

- headers are better section separators since they say what a section is about.
- horizontal rules don't have a generally accepted semantic meaning. This guide gives them one.

Use 3 hyphens without spaces:

    ---

## Tables

Extension.

-   Surround tables by one empty line.
-   Don't indent tables.
-   Surround every line of the table by pipes.
-   Align all border pipes vertically.
-   Separate header from body by hyphens except at the aligned pipes `|`.
-   Pipes `|` must be surrounded by a space, except for:
    - pipes at the header separator, which are surrounded by a hyphen `-`.
    - outer pipes which only get one space or hyphen internally.
-   Column width is determined by the longest cell in the column.
-   Left align content inside cells. In flavors where header cells determine text alignment, align only the header, and keep the body cells left aligned.

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

## Separate consecutive elements

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

## Links

### Reference-style links

- must be the last thing on the file
- must be sorted alphabetically by the ID
- don't enclose URLs by angle brackets
- align URLs and link names as in a table
- link IDs use only lowercase letters. Rationale: they are case insensitive, lowercase only is easier to write, and the readability gain of mixed case is not very big.

Good:

    [id2]     http://long-url.com
    [long id] http://a.com        "name 1"

## Emphasis

### Bold

Use double asterisk format: `**bold**`.

Rationale: more common and readable than the double underline `__bold__` form.

### Italic

Use single asterisk format: `*italic*`.

Rationale:

- more common and readable than the underscore form
- consistent with the bold format, which also uses asterisks

## Automatic links

## Automatic links without angle brackets

*Don't* use automatic links without angle brackets.

Good:

    <http://a.com>

Bad:

    http://a.com

Rationale: it is an extension, `<>` is easy to type and saner.

### Email automatic links

*Don't* use email autolinks `<address@example.com>`. Use raw HTML instead.

Rationale: the original markdown specification states it "performs a bit of randomized decimal and hex entity-encoding to help obscure your address from address-harvesting spambots". Therefore, the output is random, ugly, and as the spec itself mentions "but an address published in this way will probably eventually start receiving spam".
