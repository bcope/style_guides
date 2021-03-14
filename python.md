# Python Style Guide

<!-- TODO: need to incorporate previous work version of this document -->

## Guiding principles

### Convention over creation

My intention with this style guide is to gather into one place all the answers
to questions that I often ask myself about styling and formatting. So if
anything this will be a list of external resources first, with a few personal
exceptions second.

## Linting

### VSCode plugins

<!-- TODO: need to look into this and pick one of these once and for all -->

## Docstrings

[PEP 257](https://www.python.org/dev/peps/pep-0257/) is a little lite on details
for my taste. Follow the [Google examples here](https://sphinxcontrib-napoleon.readthedocs.io/en/latest/example_google.html).

Use triple double quotes to enclose docstrings.

## Type hinting

While I love this in principle in practice I find that type hinting everything
makes code less readable and less enjoyable to write, which leads to worse code
in my experience.

It might make sense for me to implement some partial type hinting at least in
class, method, and function parameters and return values. I admittedly need to
do some research to see if partial implementation has any real value.

Until I have a more cohesive strategy I am electing to avoid type hinting in
new files. In files where type hinting exists already I will follow the
existing patterns.

### Handling files with inconsistent type hinting

If it is quick and easy to add type hints to make the file fully type hinted, I
will do that. However, if it is not fast to add type hints I will migrate the
existing type hints into docstrings in one commit. Then I will remove the type
hints in a separate commit.

## Quotes

There are at least four different possible quote styles in Python. Here are my
notes about when to use each style.

### Single quotes

- simple strings
- bracket notation

### Double quotes

- f-strings

### Triple single quotes

- multi-line strings
- strings containing quotes

### Triple double quotes

- docstrings
- multi-line f-strings
- single line f-strings containing double quotes
