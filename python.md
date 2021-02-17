# Python Style Guide

## Guiding Principles

### Convention Over Creation

My intention with this style guide is to gather into one place all the answers
to questions that I often ask myself about styling and formatting. So if
anything this will be a list of external resources first, with a few personal
exceptions second.

## Linting

### VSCode Plugins

<!-- TODO: need to look into this and pick one of these once and for all -->

## Docstrings

Follow the [Google example here](https://sphinxcontrib-napoleon.readthedocs.io/en/latest/example_google.html).

<!-- TODO: need to incorporate previous work version of this document -->

## Type Hinting

While I love this in principle in practice I find that type hinting everything
makes code less readable and less enjoyable to write, which leads to worse code
in my experience.

It might make sense for me to implement some partial type hinting at least in 
class, method, and function parameters and return values. I admittedly need to
do some research to see if partial implementation has any real value.
