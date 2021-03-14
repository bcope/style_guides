# Markdown Style Guide

Follow the [David Anson markdown rules](https://github.com/DavidAnson/markdownlint/blob/master/doc/Rules.md)

## Linting tools

- [VSCode Extension](https://github.com/DavidAnson/vscode-markdownlint)
- [Web based](https://dlaa.me/markdownlint/)
- [CLI](https://github.com/igorshubovych/markdownlint-cli)

## VSCode settings

```json
    "[markdown]": {
        "editor.tabSize": 2,
        "editor.insertSpaces": true,
        "editor.rulers": [80, 100],
        "editor.wordWrap": "bounded",
        "editor.wordWrapColumn": 100
    },
```

## List indentation

Use two spaces to indent sub-list items in unordered lists

Yes:

```md
- item 1
  - sub list item a
  - sub list item b
- item 2
```

Use four spaces to indent sub-list items in ordered lists

Yes:

```md
1. item 1
    1. sub list item a
    1. sub list item b
1. item 2
```

<!-- TODO: provide recommendation on indenting intermingled ordered and unordered lists -->

## Wrapping text

Avoid manually wrapping text onto new lines. Instead prefer to establish syntax specific wrapping settings.

It is frustrating to update a paragraph and have to re-manually wrap lines to conform to line length. This also leads to worse commit messages.

In VSCode the `bounded` setting allows for setting a maximum line length while also handling when the viewport shrinks to a smaller width than the line length.

```json
"editor.wordWrap": "bounded",
"editor.wordWrapColumn": 100
```

## Header casing

The single H1 used to title the document should be in Title Case.

For all other headers avoid Title Case and prefer to capitalize the first word only. It is easier to follow this consistently and have the headers remain aesthetically pleasing. Sometimes headers contain a long phrase which can look clumsy in Title Case.
