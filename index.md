---
title: Markdown Style Guide
---

Readable and portable Markdown style guide.

Considers both the [original specification](http://daringfireball.net/projects/markdown/syntax) and common extensions.

After this project was started, [CommonMark](http://commonmark.org) was released.
Our decisions will also consider it since it is well specified and has a strong industry backing
(GitHub + Stack Overflow + reddit).

[Source code](https://github.com/cirosantilli/markdown-styleguide/blob/master/index.md).
This is not automatically updated with the source, but will be updated at every major change.

- a
{:toc}

# Design goals

- readable
- portable: produces the same output, or good output, across multiple implementations.
    Portability tests are carried out with the [Markdown Test Suite](https://github.com/karlcow/markdown-testsuite).
- easy to write and modify later
- diff friendly
- easy to remember and implement on editors
- provide rationale behind difficult choices.
    Every rationale section or paragraph is marked with `rationale`
    so you can skip it if you are only interested in the final decisions.

# Notable users

- [GitLab](https://github.com/gitlabhq/gitlabhq/blob/master/CONTRIBUTING.md#style-guides)
- [Vim Markdown](https://github.com/plasticboy/vim-markdown/blob/master/CONTRIBUTING.md#style)

Do you use this style guide? Add your name to [our wiki](https://github.com/cirosantilli/markdown-styleguide/wiki/Users).

Are you notable? Send a pull request.

If you are a notable user:

- you can opt to be contacted before any major changes happen to the standard.
    Please inform this on the pull request that adds you to the notable list.

- your vote on decisions will have much greater weight

You are more likely to be notable if your project:

- uses Markdown heavily. E.g.: Markdown engines, text editors, lots of markdown documentation, etc.

- is popular. Any popularity measure will be taken into account, e.g. GitHub stars,
    Google Rank, etc. 2K+ GitHub stars makes for a very strong case.

# Options system

Disputed points will be given multiple alternatives.

Features with multiple alternatives will be given single upper case letter identifiers,
and marked in key value pairs as follows: feature **Z** with 3 alternatives:

    # Option Z1
    # Option Z2
    # Option Z3

Then, for another feature **X** with two alternatives:

    # Option X1
    # Option X2

When referring to this guide, specify all alternatives as follows:

    Use the Markdown Style Guide A2 C3

to say you want feature `A` to use alternative `2` and feature `C` to use alternative `3`.

If not specified, the alternative **1** is assumed for the feature by default.

This default alternative shall be determined by popular vote.

We will attempt to give intuitive letter identifiers for each feature if one is available,
e.g. the `Line Wrapping` feature could get identifier `W`.

# Why fork Carwin

This guide was forked from [carwin/markdown-styleguide](https://github.com/carwin/markdown-styleguide/tree/9121c77bd177a3ade6713d50ab1228782d7c02a7)
because there were many important points in which we disagreed. This guide proposes:

- softer limits on wrapping
- lists indented with 4 spaces, not 2
- ordered lists only with `1.`
- italics with `*it*`, not `_it_`
- tables have pipes before and after

The general structure of the guide was kept, but almost every line was modified,
and many additions were made.

# General rules

## File

### File extension

Use `.md`.

Rationale: why not `.mkd` or `.markdown`?

- shorter
- more popular
- does not have important conflicts

### File name

Prefer to base the file name on the top-header level:

- replace upper case letters with lower case
- strip articles (`the`, `a`, `an`) and prepositions (`from`, `to`)
- replace punctuation and white space characters by hyphens
- replace consecutive hyphens by a single hyphen
- strip surrounding hyphens

Good:

    file-name.md

Bad, multiple consecutive hyphens:

    file--name.md

Bad, surrounding hyphens:

    -file-name-.md

Rationale: why not underscore or camel case? Hyphens are the most popular URL separator today,
and markdown files are most often used in contexts where:

- there are hyphen separated HTML files in the same project, possibly the same directory as the markdown files.
- filenames will be used directly on URLs. E.g.: GitHub blobs.

## Space

*Don't* use 2 or more consecutive empty lines, that is,
more than two consecutive newline characters,
except where they must appear literally such as in code blocks.

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

Rationale: multiple empty lines occupy more vertical screen space,
and do not significantly improve readability.

## Line wrapping

### Wrap at logical intra-sentence points

### Option W1

Try to keep lines under 80 characters by breaking large paragraphs logically at points such as:

- sentences: after a period `.`, question `?` or exclamation mark `!`
- [clauses](http://www.oxforddictionaries.com/words/clauses):
    after words like `and`, `which`, `if ... then`, commas `,`
- large [phrases](http://www.oxforddictionaries.com/words/phrases)

It is acceptable to have a line longer than 80 characters,
but keep in mind that long sentences are less readable
and look worse in tools such as `git diff`.

Set your editor to wrap lines visually for Markdown in case a large line is present.

Good:

    This is a very very very very very very very very very very very very very long not wrapped sentence.
    Second sentence of of the paragraph,
    third sentence of a paragraph
    and the fourth one.

Rationale:

-   Diffs look better, since a change to a clause shows up as a single diff line.
-   Occasional visual wrapping does not significantly reduce the readability of Markdown,
    since the only language feature that can be indented to indicate hierarchy are nested lists.
-   At some point GitHub translated single newlines to line breaks in READMEs,
    and still does so on comments.
    Currently there is no major engine which does it, so it is safe to use newlines.
-   Some tools are not well adapted for long lines, e.g. Vim and `git diff` will not wrap lines by default.
    This can be configured however via `git config --global core.pager 'less -r'` for Git and `set wrap` for Vim.

Downsides:

- requires considerable writer effort, specially when modifying code.
- Markdown does not look like the rendered output, in which there are no line breaks.
    Manual line breaking can make the Markdown more readable than the rendered output,
    which is bad because it gives a false sense of readability encouraging less
    readable long paragraphs.

### Don't wrap

### Option W2

Don't wrap lines.

### Wrap at spaces

### Option W3

Always wrap at the end of the first word that exceeds 80 characters.

Rationale: source code becomes is very readable and text editors support it automatically.
But diffs will look bad, and changing lines will be hard.

### Wrap at sentences

### Option W4

Similar to Option W1, but easier for people to follow since the rule is simple:
break after the period.

Notable occurrence: [ProGit 2](https://raw.githubusercontent.com/progit/progit2/5c285553c0605342339284981a9bb8a6c4e7c18e/book/01-introduction/1-introduction.asc).

## Code

### Dollar signs in shell code

*Don't* prefix shell code with dollar signs `$`
unless you will be showing the command output on the same code block.

If the goal is to clarify what the language is, do it on the preceding paragraph.

Rationale: harder to copy paste, noisier to read.

Good:

    echo a
    echo a > file

Bad:

    $ echo a
    $ echo a > file

Good, shows output:

    $ echo a
    a
    $ echo a > file

Good, language specified on preceding paragraph:

    Use the following Bash code:

    echo a
    echo a > file

### What to mark as code

Use code blocks or inline code for:

-   executable. E.g.:

        `gcc` is the best compiler available.

    Differentiate between tool and the name of related projects. E.g.: `gcc` vs GCC.

-   file paths

-   version numbers

-   capitalized explanation of abbreviations:

        xinetd stands for `eXtended Internet daemon`

-   other terms related to computers that you don't want to add to your dictionary

Don't mark as code:

-   names of projects. E.g.: GCC

-   names of libraries. E.g.: libc, glibc

### Spelling and grammar

Use correct spelling and grammar.

Prefer writing in English, and in particular American English.
Rationale: American English speakers have the largest GDP,
specially in the computing industry.

Use markup like URL or code on words which you do not want to add to your dictionary
so that spell checkers can ignore them automatically.

Beware of case sensitive spelling errors, in particular for project, brand names or abbreviations:

- Good: URL, LinkedIn, DoS attack
- Bad: `url`, `Linkedin`, `dos attack`

When in doubt, prefer the same abbreviation as used on Wikipedia.

Avoid informal contractions:

- Good: biography, repository, directory
- Bad: `bio`, `repo`, `dir`

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

    `Setex` headers are more visible, but good visibility can be achieved for `atx-style` headers
    by configuring your editor to syntax highlight them.

-   Include a space between the `#` and the text of the header.

-   Headers must be surrounded by one empty line except at the beginning of a file.

-   Headers must *not* have spaces preceding the number sign.

-   *Don't* use two headers with the same content in the same markdown file.

    Rationale: many markdown engines generate IDs for headers based on the header content.

-   Don't skip header levels.

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

If you target HTML output, write your documents so that it will have one
and only one `h1` element as the first thing in it that serves as the title of the document.
This is the HTML top-level header.

How this `h1` is produced may vary depending on your exact technology stack:
some stacks may generate it from metadata, for example Jekyll through the front-matter.

Storing the top-level header as metadata has the advantage that it can be reused elsewhere more easily,
e.g. on a global index, but the downside lower portability portable.

If your target stack does not generate the top-level header in another way,
include it in your markdown file. E.g., GitHub.

Top-level headers on index-like files such as `README.md` or `index.md`
should serve as a title for their parent directory.

Downsides of top-level headers:

-   take up one header level. This means that there are only 5 header levels left,
    and each new header will have one extra `#`, which looks worse and is harder to write.

-   duplicate filename information, which most often can already be seen on a URL.
    In most cases, the filename can be trivially converted to a top-level,
    e.g.: `some-filename.md` to `Some filename`.

Advantages of top-level headers:

- more readable than URL's, especially for non-technically inclined users.

### Header case

-   Use an upper case letter as the first letter of a header,
    unless it is a word that always starts with lowercase letters, e.g. computer code.

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

    As an exception, [title case](http://en.wikipedia.org/wiki/Title_case#Title_case)
    may be optionally used for the [top-level header](#top-level-header).
    Use this exception sparingly, in cases where typographical perfection is important,
    e.g.: `README` of a project.

    Rationale: why not [Title case](http://en.wikipedia.org/wiki/Title_case#Title_case) for all headers?
    It requires too much effort to decide if edge-case words should be upper case or not.

### End of a header

Indicate the end of a header's content that is not followed by a new header by an horizontal rule:

    # Header

    Content

    ---

    Outside header.

### Header length

Keep headers as short as possible.

Instead of using a huge sentence, make the header a summary to the huge sentence,
and write the huge sentence as the first paragraph beneath the header.

Rationale: it is easier to refer to the header later,
specially if automatic IDs or a TOC are generated by the implementation.

Good:

    # Huge header

    Huge header that talks about a complex subject.

Bad:

    # Huge header that talks about a complex subject

### Trailing punctuation

*Don't* add a trailing colon `:` to headers.

Rationale: every header is an introduction to what is about to come next,
which is exactly the function of the colon.

*Don't* add a trailing period `.` to headers.

Rationale: every header consists of a single short sentence,
so there is not need to add a sentence separator to it.

Good:

    # How to do make omelet

Bad:

    # How to do make omelet:

Bad:

    # How to do make omelet.

### Header synonyms

Headers serve as an index for users searching for keywords.

For this reason, you may want to give multiple keyword possibilities for a given header.

To do so, simply create a synonym header with empty content just before its main header.

E.g.:

    # Purchase

    # Buy

    You give money and get something in return.

Every empty header with the same level as the following one is assumed to be a synonym.
This is not the case if levels are different:

    # Animals

    ## Dog

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

Prefer lists only with the marker `1.` for ordered lists,
unless you intend to refer to items by their number in the same markdown file or externally.

Prefer unordered lists unless you intent to refer to items by their number.

Best, we will never refer to the items of this list by their number:

    - a
    - c
    - b

Better, only `1.`:

    1. a
    1. c
    1. b

Worse, we will never refer to the items of this list by their number:

    1. a
    2. c
    3. b

Acceptable, refer to them in the text:

    The ouput of the `ls` command is of the form:

        drwx------  2 ciro ciro        4096 Jul  5  2013 dir0
        drwx------  4 ciro ciro        4096 Apr 27 08:00 dir1
        1           2

    Where:

    1. permissions
    2. number of files directory contains

Acceptable, meant to be referred by number from outside of the markdown file:

    Terms of use.

    1. I will not do anything illegal.
    2. I will not do anything that can harm the website.

Rationale:

-   If you want to change a list item in the middle of the list,
    you don't have to modify all items that follow it.

    Diffs will show only the significant line which was modified.

-   Content stays aligned without extra effort if the numbers reach 2 digits. E.g.: the following is not aligned:

        9. a
        10. b

-   References break when a new list item is added. To reduce this problem:

    - keep references close to the list so authors are less likely to forget to update them
    - when referring from an external document, always refer to an specific version of the markdown file

### Spaces after marker

-   If the content of every item of the list is fits in a single paragraph, use **1** space.

    Indent wrapped lines 4 spaces deeper than their parent.

-   Otherwise, for every item of the list:

    - use **3** spaces for unordered lists.
    - use **2** spaces for ordered lists.
        One less than for unordered because the marker is 2 chars long.

Good:

    - a
    - b
    - paragraph
        with a wrapped line.

<!-- -->

    1. a
    1. b

<!-- -->

    -   a

        par

    -   b

            code

    -   c

<!-- -->

    1.  a

        par

Bad, single line content only:

    -   a
    -   b

Bad, line break but indented only 2 spaces deeper:

    - First part of
      line break.

Bad, content that does not fit in a single line:

    - a

        par

<!-- -->

    - a

            code

<!-- -->

    - a
        - nested list

#### Rationale: why not always single space?

Because important engines such as Marked and Kramdown indent relative to the last character,
and are currently reluctant to even add options that allow to change that behavior,
see: <https://github.com/chjj/marked/issues/227>, <https://github.com/gettalong/kramdown/issues/121>.

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

This divergence probably happened because all the examples
of the original markdown documentation are of the above form.

Most major engines however don't add the two extra spaces.

### Indented lists

-   Indented list items and their content by 4 spaces further than their parent.
    The first level has no indent.

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

### Lists and empty lines

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
                and line break.
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

-   Avoid multi-paragraph items inside lists without `<p>`,
    as this adds `<p>` to one element of the list,
    and some style sheets like GitHub's add an extra vertical space because of that.

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

## Case of first letter of list item

If the list can be replaced by a long phrase separated with commas,
start list items with lower case letters as you would if you were using commas.
Only add a final period if at least one of the list items contains multiple sentences.

If the list can be replaced by several sentences,
start list items with upper case letters and add a final period.

Good:

    I want to eat:

    - apples
    - bananas
    - grapes

because it could be separated with commas as in:

    I want to eat apples, bananas and grapes.

Good:

    To ride a bike you have to:

    - get on top of the bike. This step is easy.
    - put your foot on the pedal.
    - gake the pedal turn. This is the most fun part.

Good:

    # How to ride a bike

    - Get on top of the bike.
    - Put your feet on the pedal.
    - Make the pedal turn.

because it could be replaced by several sentences:

    # How to ride a bike

    Get on top of the bike. Put your feet on the pedal. Make the pedal turn.

## Definition lists

Extension.

*Don't* use definition lists as they are not part of the original implementation,
and are not implemented by all major engines.

Instead, use either:

-   Formated lists of the form:

    - item to be defined has a special span format such as bold, italic or link
    - colon `:` and a space
    - aligned definitions

    Good:

        - **apple**: red fruit
        - **dog**:   noisy animal

    <!-- -->

        - [apple](http://apple.com): red fruit
        - [dot](http://dog.com): red fruit

    Bad, no colon:

        - **apple** red fruit
        - **dog**   noisy animal

    Bad, space between term and colon:

        - **apple** : red fruit
        - **dog** :   noisy animal

    Bad, definitions not aligned:

        - **apple**: red fruit
        - **dog**: noisy animal

-   Headers.

    Good:

        # Apple

        Red fruit

        # Dog

        Noisy animal

## Code blocks

### Fenced only

### Option C1

Only use fenced code blocks.

Comparison to indented code blocks:

- disadvantage: not part of the original markdown, thus less portable, but added to CommonMark.
- advantage: many implementations, including GitHub's, allow to specify the code language with it

*Don't* indent fenced code blocks.

Always specify the language of the code is applicable.

Good:

    ```ruby
    a = 1
    ```

Bad:

    ```
    a = 1
    ```

### Indented only

### Option C2

Only use indented code blocks.

Indent indented code blocks with 4 spaces.

---

Code blocks must be surrounded by one empty line.

Prefer to end the phrase before a code block with a colon `:`.

Good:

    Use this code to blow up your PC:

        sudo rm -rf /

Bad, no colon

    Use this code to blow up your PC

        sudo rm -rf /

## Horizontal rules

*Don't* use horizontal rules except to indicate the [End of a header](#end-of-a-header).

Rationale:

- headers are better section separators since they say what a section is about.
- horizontal rules don't have a generally accepted semantic meaning.
    This guide gives them one.

Use 3 hyphens without spaces:

    ---

## Tables

Extension.

- Surround tables by one empty line.
- Don't indent tables.
- Surround every line of the table by pipes.
- Align all border pipes vertically.
- Separate header from body by hyphens except at the aligned pipes `|`.
- Pipes `|` must be surrounded by a space, except for outer pipes
    which only get one space internally, and pipes of the hyphen separator line.
- Column width is determined by the longest cell in the column.

Good table:

    Before.

    | h    | Long header |
    |------|-------------|
    | abc  | def         |
    | abc2 | def2        |

    After.

Rationale:

- unaligned tables tables are easier to write, but aligned tables are more readable,
    and people read code much more often than they edit it.
- preceding pipes make it easier to determine where a table starts and ends.
    Trailing pipes make it look better because of symmetry.
- there exist tools which help keeping the table aligned.
    For example, Vim has the [Tabular plugin](https://github.com/godlygeek/tabular) which allows to align the entire table with `:Tabular /|`.
- why no spaces around pipes of the hyphen separator line, i.e.: `|---|` instead of `| - |`?
    No spaces looks better, works on GitHub. Downside: harder to implement automatic alignment in editors,
    as it requires a special rule for the separator line.

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
    [text][name]

Bad:

    ** bold **
    ` code `
    [ link ]( http://a.com )
    [text] [name]

For inline code in which the space is crucial:

- explain in writing that the spaces must be there
- add something after the space if possible

Good:

    Use the hyphen marker followed by one space `- a`  for unordered lists.

Rationale: most browsers don't render the surrounding spaces nor add them to the clipboard on copy.

## Links

### Reference-style links

Links:

-   use the trailing `[]` on implicit links.

    Good:

        [a][]

    Bad:

        [a]

    Rationale: while omitting `[]` works on most major implementations,
    it is not specified in the documentation not implemented in the original markdown.

Definitions:

- must be the last thing on the file
- must be sorted alphabetically by the ID
- don't enclose URLs by angle brackets
- align URLs and link names as in a table
- link IDs use only lowercase letters. Rationale: they are case insensitive,
- lowercase only is easier to write, and the readability gain of mixed case is not very big.

Good:

    [id2]     http://long-url.com
    [long id] http://a.com        "name 1"

Bad, not ordered by id:

    [b] http://a.com
    [a] http://b.com

Bad, not aligned:

    [id] http://id.com
    [long id] http://long-id.com

### Single or double quote titles

Use double quotes, *not* single quotes.

Rationale: single quotes do not work in all major implementations, double quotes do.

## Emphasis

### Bold

Use double asterisk format: `**bold**`.

Rationale: more common and readable than the double underline `__bold__` form.

### Italic

Use single asterisk format: `*italic*`.

Rationale:

- more common and readable than the underscore form
- consistent with the bold format, which also uses asterisks

### Uppercase for emphasis

*Don't* use uppercase for emphasis: use emphasis constructs like **bold** or *italic* instead.

Rationale: CSS has `text-transform:uppercase` which can easily achieve the same effect consistently
across the entire website if you really want uppercase letters.

### Emphasis vs headers

*Don't* use emphasis elements (bold or italics) to introduce a multi line named section: use headers instead.

Rationale: that is exactly the semantic meaning of headers,
and not necessarily that of emphasis elements. As a consequence,
many implementations add useful behaviors to headers and not to emphasis elements,
such as automatic `id` to make it easier to refer to the header later on.

Good:

    # How to make omelets

    Break an egg.

    ...

    # How to bake bread

    Open the flour sack.

    ...

Bad:

    **How to make omelets:**

    Break an egg.

    ...

    **How to bake bread:**

    Open the flour sack.

    ...

## Automatic links

### Automatic links without angle brackets

-   *Don't* use automatic links without angle brackets.

    Good:

        <http://a.com>

    Bad:

        http://a.com

    Rationale: it is an extension, `<>` is easy to type and saner.

-   If you want literal links which are not autolinks, enclose them in code blocks. E.g.:

        `http://not-a-link.com`

    Rationale: many tools automatically interpret any word starting with `http` as a link.

### Content of automatic links

All automatic links must start with the string `http`.

In particular, *don't* use relative automatic links.
Use bracket links instead for that purpose.

Good:

    [file.html](file.html)

Bad:

    <file.html>

Good:

    <https://github.com>

Bad:

    <github.com>

Rationale: it is hard to differentiate automatic links from HTML tags.
What if you want a relative link to a file called `script`?

### Email automatic links

*Don't* use email autolinks `<address@example.com>`. Use raw HTML instead.

Rationale: the original markdown specification states it:

> "performs a bit of randomized decimal and hex entity-encoding
> to help obscure your address from address-harvesting spambots".

Therefore, the output is random, ugly, and as the spec itself mentions:

> but an address published in this way will probably eventually start receiving spam
