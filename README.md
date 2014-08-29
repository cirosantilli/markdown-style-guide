# Markdown Style Guide

Readable and portable Markdown style guide: <http://www.cirosantilli.com/markdown-styleguide>

Contributors:

-   The main source file is [index.md](index.md).

-   Hosted on GitHub pages so it gets the Kramdown generated TOC.

-   Deployed as a submodule of: <https://github.com/cirosantilli/cirosantilli.github.io>

    To develop, you can either:

    -   modify it directly, view on GitHub, and hope it renders the same as Kramdown on the website.
        It usually does.

    -   play it safer and do:

            git clone --recursive https://github.com/cirosantilli/cirosantilli.github.io
            cd cirosantilli.github.io
            bundle install
            bundle exec jekyll serve --watch
            firefox http://localhost:4000/markdown-styleguide
