# SQL Style Guide

## Guiding principles

### Version control first

Many of the choices we've made were made in order to make reviewing pull requests easier.

With this in mind, formatting changes to existing files should be made in separate commits and pull requests than changes of substance.

### Overlapping styles

When possible and where it makes sense we try to align style recommendations across languages. You will find some overlapping styles across SQL and Python which is very intentional. Habits are hard to break, so we're leveraging that in our style choices.

### Comment intentions

Use rigorous comments to let future readers know what you were trying to accomplish. Explain your goal and intent of conditions. Sometimes it might makes sense to include anecdotes about the data being referenced but only in addition to what you were trying to do. In theory the person reading the query later will have some domain knowledge about the underlying data structures (or can do some sleuthing create the necessary understanding). But if they don't have access to you (or your notes) they won't be able to recreate why you excluded or included something.

## Casing

### Uppercase keywords

- Clauses: `SELECT`, `FROM`, `WHERE`, `GROUP BY`, `HAVING`, `ORDER BY`, `LIMIT`, `OFFSET`
- Functions such as: `SUM`, `COUNT`, `DATE_SUB`, `IF`
- Operators like: `LIKE`, `ON`, `AND`, `OR`, `NOT`
- Other keywords like: `AS`, `INTERVAL`

These are some examples but the overall point is to uppercase words that are performing some functionality.

### Snake case for everything else

- Variables: `@my_variable`
- Column Aliases: `AS total_amount`

## Spacing

### Spaces around operators

- Use a single space on both sides of operators such as: `-`, `+`, `*`, `=`, `<`, `>`, `<=`, `>=`, `<=>`, `!=`

### A space after commas

Use a single space after non-line-ending commas. This increases readability.

## Indentation

Use a soft tab of four spaces for each level of indentation.

### One indent after each clause keyword

Increase the indent level on a new line after each major clause keyword: `SELECT`, `FROM`, `WHERE`, `GROUP BY`, `HAVING`, `ORDER BY`, `LIMIT`, `OFFSET`. This makes it very easy to visually scan for the next section of the query.

### Increase indent for secondary conditions in joins

Most joins only have one condition in the `ON` clause. When there are multiple conditions, increase the indent to make this visually apparent.

Example:

```sql
    LEFT JOIN customer c
    ON o.customer_id = c.id
        # don't joined deleted records
        AND c.deleted = 0
```

### Increase indent inside of parenthetical statement on a newline

Example:

```sql
    LEFT JOIN (
        SELECT
            ...
        FROM
            ...
    ) x
    ON ...
```

## Line breaks

### Between each field in SELECT clause

Each field should begin on a new line. Sometimes it makes sense to wrap the field onto multiple lines when it exceeds max line length and contains obvious points at which to start a new line.

### Between JOIN and ON lines

Start ON statements on a new line after the JOIN statement for visual clarity. It makes it easier to see how the joined table is being aliased and it makes it easier to see how the ON statement is working. This also allows for a comment line between these two when the ON statement is confusing.

### Between each condition in WHERE clause

Each condition should start on a new line. Sometimes if an exclusion for a query is intuitively one exclusion but requires two conditions that make less sense when separated you can include them on one line if they are both short, but you should avoid this.

### Between each portion of GROUP BY, HAVING, and ORDER BY

At this point I've decided to start new ideas on new lines and this should be applied to these sections out of consistency and visual clarity.

### After opening parenthetical containing long statement

Start a new line (and increase indent) after an opening parenthetical statement that will exceed max line length. Notable examples of this:

- Joined subselect
- Switching between AND and OR conjunctions
- Long IF statement with complex conditions

## Comments

### Types of comments

- `-- ` Use to comment out code that is not being used.
- `# ` Use to include explanations about what the code is meant to do.
- `/*  */` Use for multi-line explanations in advance of the code. Avoid using in the middle of a query.

### Comment for all WHERE clause conditions

Every condition in your WHERE clause is important. There are two things that you should make sure and explain about each of your WHERE conditions:

1. What are you attempting to accomplish and why?
1. Is there anything untoward about the underlying data that someone that is familiar with the data structure couldn't intuit?

```sql
SELECT
    c.id,
    SUM(o.amount) AS total_order_amount
FROM
    order o
    LEFT JOIN customer c
    ON o.customer_id = c.id
        AND c.deleted = 0
    # avoid joining the whole table unnecessarily
    LEFT JOIN (
        SELECT
            p.id,
            p.type
        FROM
            product p
    ) p
    ON o.product_id = p.id
WHERE
    p.type IN ('trinket')
GROUP BY
    YEAR(o.date)
HAVING
    total_order_amount > 10000
ORDER BY
    total_order_amount DESC
LIMIT
    100
OFFSET
    200
```

## Aliasing

You should alias your tables, even if there is only one referenced table in a query. This enables adding in joined tables after the fact without having to go back and make changes to existing code.

### Use table acronym where possible

Most of the time you should be able to use the acronym of the table name as the table alias.

## Query writing best practices

### Avoid hard coded date ranges that may change

Instead use variables. This makes it clear when looking at the query that there is a date range that is relevant to the results.
