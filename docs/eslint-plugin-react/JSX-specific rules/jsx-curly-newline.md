# Enforce linebreaks in curly braces in JSX attributes and expressions. (react/jsx-curly-newline)

Many style guides require or disallow newlines inside of jsx curly expressions.

**Fixable:** This rule is automatically fixable using the `--fix` flag on the command line.

## Rule Details

This rule enforces consistent linebreaks inside of curlies of jsx curly expressions.

## Rule Options

This rule accepts either an object option:

```ts
{
  multiline: "consistent" | "forbid" | "require", // default to 'consistent'
  singleline: "consistent" | "forbid" | "require", // default to 'consistent'
}
```
Option `multiline` takes effect when the jsx expression inside the curlies occupies multiple lines.

Option `singleline` takes effect when the jsx expression inside the curlies occupies a single line.

* `consistent` enforces either both curly braces have a line break directly inside them, or no line breaks are present.
* `forbid` disallows linebreaks directly inside curly braces.
* `require` enforces the presence of linebreaks directly inside curlies.

or a string option:

* `consistent` (default) is an alias for `{ multiline: "consistent", singleline: "consistent" }`.
* `never` is an alias for `{ multiline: "forbid", singleline: "forbid" }`

or an

### consistent (default)

When `consistent` or `{ multiline: "consistent", singleline: "consistent" }` is set, ```the following patterns are considered warnings:```

```jsx
<div>
  { foo
  }
</div>

<div>
  {
    foo }
</div>

<div>
  { foo &&
    foo.bar
  }
</div>
```

```The following patterns are **not** warnings:```

```jsx
<div>
  { foo }
</div>

<div>
  {
    foo
  }
</div>
```

### never

When `never` or `{ multiline: "forbid", singleline: "forbid" }` is set, ```the following patterns are considered warnings:```

```jsx
<div>
  {
    foo &&
    foo.bar
  }
</div>

<div>
  {
    foo
  }
</div>

<div>
  { foo
  }
</div>
```

```The following patterns are **not** warnings:```

```jsx
<div>
  { foo &&
    foo.bar }
</div>

<div>
  { foo }
</div>
```

## require

When `{ multiline: "require", singleline: "require" }` is set, ```the following patterns are considered warnings:```

```jsx
<div>
  { foo &&
    foo.bar }
</div>

<div>
  { foo }
</div>

<div>
  { foo
  }
</div>
```

```The following patterns are **not** warnings:```

```jsx
<div>
  {
    foo &&
    foo.bar
  }
</div>

<div>
  {
    foo
  }
</div>
```


## When Not To Use It

You can turn this rule off if you are not concerned with the consistency of padding linebreaks inside of JSX attributes or expressions.