# Python Style Guide

<!-- TOC -->

- [Guiding principles](#guiding-principles)
  - [Convention over creation](#convention-over-creation)
  - [Version control first](#version-control-first)
  - [Leave things better than you found them](#leave-things-better-than-you-found-them)
  - [Be consistent](#be-consistent)
- [Editing](#editing)
  - [VSCode plugins](#vscode-plugins)
- [Formatting](#formatting)
  - [Docstrings](#docstrings)
  - [Line length](#line-length)
  - [Indentation](#indentation)
    - [Never align with opening delimiter](#never-align-with-opening-delimiter)
    - [One line or many](#one-line-or-many)
  - [Closing delimiters & trailing commas](#closing-delimiters--trailing-commas)
  - [Quotes styles](#quotes-styles)
    - [Single quotes](#single-quotes)
    - [Double quotes](#double-quotes)
    - [Triple single quotes](#triple-single-quotes)
    - [Triple double quotes](#triple-double-quotes)
- [Syntax](#syntax)
  - [Type hinting](#type-hinting)
    - [Handling files with inconsistent type hinting](#handling-files-with-inconsistent-type-hinting)
  - [String formatting](#string-formatting)
  - [Function / method length](#function--method-length)
  - [Class methods](#class-methods)
- [Naming](#naming)
  - [Avoid abbreviations](#avoid-abbreviations)
  - [Separate words in functions and variables with underscores](#separate-words-in-functions-and-variables-with-underscores)
- [Testing](#testing)

<!-- /TOC -->

## Guiding principles

### Convention over creation

My intention with this style guide is to gather into one place all the answers to questions that I often ask myself about styling and formatting. So if anything this will be a list of external resources first, with a few personal exceptions second.

I try to follow [PEP8](https://www.python.org/dev/peps/pep-0008/), [PEP20](https://www.python.org/dev/peps/pep-0020/), and [Google's Python Style Guide](https://google.github.io/styleguide/pyguide.html). This document contains deviations from those sources or clarifications meant for my specific context.

I strive to write pythonic code that other Pythonistas would not shudder to read. That said, I do have some non-pythonic personal preferences. I attempt to call these out as such (at least where I am aware of their opinionated quality).

### Version control first

Many of the choices I've made were made in order to make reviewing pull requests easier and reviewing history more clear.

With this in mind, formatting changes to existing files should be made in separate commits from changes of substance.

### Leave things better than you found them

Whenever possible, fix the formatting of code you are working near. Remember to commit those changes separately though.

### Be consistent

If you are adding to existing code and can't reformat all of it, [keep consistent with what is there.](https://google.github.io/styleguide/pyguide.html#4-parting-words)

## Editing

I use VSCode to write and edit Python. I run Python in the terminal either directly or by way of a docker run command. I do some experimenting in Jupyter Notebooks.

### VSCode plugins

<!-- TODO: need to look into this and pick one of these once and for all -->

## Formatting

### Docstrings

[PEP 257](https://www.python.org/dev/peps/pep-0257/) is a little lite on details for my taste. Follow the [Google examples here](https://sphinxcontrib-napoleon.readthedocs.io/en/latest/example_google.html).

Use triple double quotes to enclose docstrings.

### Line length

While [PEP?]() <!-- TODO: look this up and fix --> recommends a maximum line length of 80 I have chosen to go with a maximum line length of 100. Where sensible I still attempt to observe a preferred max line length of 80. That said, I use a lot of list comprehensions and these often extend to a column somewhere between 80 and 100 and they are more confusing when broken across lines.

The trailing line break is included in the counts above.

### Indentation

This is where I differ most extremely with PEP8 and typical pythonic code. I concluded the following for two main reasons: 1) to allow for a minimal amount of difference across languages, and 2) to increase visual alignment of opening and closing delimiters.

#### Never align with opening delimiter

No:

```python
# Aligned with opening delimiter.
foo = long_function_name(var_one, var_two,
                         var_three, var_four)
```

A change to the function name would require changes on two or more lines rather than one.

#### One line or many

Yes:

```python
foo = long_function_name(with_vars, that_fit, within_line_length)
```

Yes:

```python
foo = long_function_name(
    with_vars,
    that_do_not,
    fit_within,
    line_length=100,
)
```

If the function call does not fit on one line within the line maximum then put all the variables on separate lines with a trailing comma on the final variable and the closing delimiter at same indent as indent of line of opening delimiter. This standard should be applied to function definitions as well as other similar situations.

### Closing delimiters & trailing commas

Yes:

```python
my_dict = {
    attr_1: 'one',
    attr_2: 'per',
    attr_2: 'line',
}
```

Putting closing delimiters on same indent level as indent of line of opening delimiter makes for easier visual scanning to the end of a code block.

Add trailing comma to last list item (or dictionary attribute, function parameter, ect) when they are on separate lines.

### Quotes styles

There are at least four different possible quote styles in Python. Here are my notes about when to use each style.

#### Single quotes

- simple strings
- bracket notation

#### Double quotes

- f-strings

#### Triple single quotes

- multi-line strings
- strings containing single quotes

#### Triple double quotes

- docstrings
- multi-line f-strings
- single line f-strings containing double quotes

## Syntax

### Type hinting

While I love this in principle in practice I find that type hinting everything makes code less readable and less enjoyable to write, which leads to worse code in my experience.

It might make sense for me to implement some partial type hinting at least in class, method, and function parameters and return values. I admittedly need to do some research to see if partial implementation has any real value.

Until I have a more cohesive strategy I am electing to avoid type hinting in new files. In files where type hinting exists already I will follow the existing patterns.

#### Handling files with inconsistent type hinting

If it is quick and easy to add type hints to make the file fully type hinted, I will do that. However, if it is not fast to add type hints I will migrate the existing type hints into docstrings in one commit. Then I will remove the type hints in a separate commit.

### String formatting

Use f-strings where possible. Where f-strings are not an option use the `.format` string method with keyword arguments. These are the most clear versions of string formatting.

### Function / method length

I have heard people say that if a function's length is over 5 lines long then it's probably too long. I think that this is true in many cases but certainly not all. I think it's a good visual test to apply to your code to quickly determine if you might have a code smell.

### Class methods

Prefer methods with return values that avoid side-effects where possible. It is much easier to write tests for these methods.

## Naming

### Avoid abbreviations

### Separate words in functions and variables with underscores

This is just a restatement of what can be found in [PEP?]()<!-- TODO: find and link to correct reference -->. For variable and function names use `snake_case`.

## Testing

I use pytest for testing as there seems to be some consensus around this as a best practice.
