# SASS Styles — Typography

Define fonts once, use everywhere

# Installation

```
npm install sass-styles-typography
```

# Usage

As early as possible, include:
```scss
// entry.scss
@use "my-typography-styles" as m-t-s;
@use "sass-styles/typography" with (
  $styles: m-t-s.$styles,
  $sizes: m-t-s.$sizes,
  $weights: m-t-s.$weights,
  $families: m-t-s.$families,
);

@use "base";
```
```scss
// _base.scss
@use "sass-styles/typography" as t;

body {
  @include t.style(body);
}
```
```scss
// _my-typography-styles.scss
$families: (/* family names */);
$sizes: (/* size matching */);
$weights: (/* weight naming */);
$styles: (/* rule definitions */);
```


# Options

## $root-font-px-size

A Number

## $length-unit

`px`, `rem`, or `rem-px`

Note: whichever unit is chosen,
unitless length values are assumed to be in `px`.

## $families

## $sizes

## $weights

## $styles


# “@mixin”s

## style

## rule


# “@function”s

## get-value

When `get`ting `size` you may also pass `$unit` as a third parameter
to explicitly request eithr the `px` or `rem` values.
By default this will return in the same unit as `$length-unit`,
or `rem` if `$length-unit` is `rem-px`.


# FAQ

- [I get the error: Error: Can't find stylesheet to import](#i-get-the-error-error-cant-find-stylesheet-to-import)
- [My version of SASS doesn’t have @use and I can’t upgrade](#my-version-of-sass-doesnt-have-use-and-i-cant-upgrade)

## I get the error: Error: Can't find stylesheet to import

If you have installed SASS Typography via npm or yarn you will
need to add `--load-path=node_modules` to your call too sass.\
Something like: `sass app.scss app.css --watch --load-path=node_modules`

Alternatively you can copy the `_t.scss` file into your own file directory.
Then you can `@use` that file directly.
However, this means you will need to do updates manually.

## My version of SASS doesn’t have @use and I can’t upgrade

This should be fine, and should work as normal without the initial `@use`.
The only issue may be that you now have functions with less readable names,
if this becomes an issue for many people I will look into making less clashy
aliases for mixins and functions.
