# SASS Styles — Typography

Define fonts once, use everywhere

## Installation

```
npm install sass-styles-typography
```

## Modules

There are various `@use`able modules included in this package. These are:
- `sass-styles-typography`: `style` mixin and accompanying tools
- `sass-styles-typography/font-family-sets`: various well-defined `font-family` sets


### Usage

Assuming `_my-typography-styles.scss` exists and contains your font styles, something like:
```scss
// _my-typography-styles.scss
$families: (/* family names */);
$sizes: (/* size matching */);
$weights: (/* weight naming */);
$styles: (/* rule definitions */);
```

then as early as possible include:
```scss
// entry.scss
@use "my-typography-styles" as m-t-s;
@use "sass-styles-typography" with (
  $styles: m-t-s.$styles,
  $sizes: m-t-s.$sizes,
  $weights: m-t-s.$weights,
  $families: m-t-s.$families,
);

@use "some-styles";
```

This has primed the library for later usage:
```scss
// _some-styles.scss
@use "sass-styles-typography" as t;
body {
  @include t.style(body);
}
```


### Options

#### $root-font-px-size

A Number

#### $length-unit

`px`, `rem`, or `rem-px`

Note: whichever unit is chosen,
unitless length values are assumed to be in `px`.

#### $families

When using `family:` in a style, the value refers to one of the families defined here.
This allows you to name families by their use-case so that if branding changes further
down the line you only need to update the `font-family` here.

This list of families is also used for `weights` and `sizes` further along.

**example**

```scss
$families: (
  body: times, serif,
  heading: arial, sans-serif,
);
```

#### $sizes

Fonts come in all different shapes and sizes, and sometimes a font-size for one font is
not the same as another font. So if, for example, you found that the heading font needed
to be 0.95 times the size of the body font, you could set up the sizes object as shown
here, then using the same size will actually display the texts at the same size:

**example**

```scss
// to even the sizes out, you can do one of the following:

// you can display headings slighly smaller:
$sizes: (
  body: 1,
  heading: 0.95,
);

// or you can display body slighly larger:
$sizes: (
  body: 1.05,
  heading: 1,
);
```

#### $weights

Similarly to sizes, but here we will likely display multiple weights.
Websites often use a minimal number of font weights, but maybe for bold text you want
`600` on one font, and `700` on another. And maybe the “normal” weight for body text is too
bold, so you want it to be `300`, rather than `400`. This allows you to use the nice named
font weights while: keeping control of how everything looks; and enforcing the
`font-weight`s being used.

**example**

```scss
$weights: (
  body: (
    normal: 300,
    bold: 600,
  ),
  heading: (
    normal: 400,
    bold: 700,
  ),
);
```

#### $styles

And here you define all of your named styles:

```scss
$styles: (
  blog-title: (
    family: heading,
    size: 24,
    weight: normal,
    tracking: -0.01,
  ),
  section-heading: (
    extend: blog-title,
    size: 20,
    weight: bold,
  ),
  body: (
    family: body,
    size: 16,
    weight: normal,
  ),
);
```

Note the usage of typographic words, and abbreviations for various keys.
These are purely sugar and are aliases of the real names, you may use the
vanilla CSS names if you prefer.
For those of you who like the sugar, here is a list of the aliases:

- `weight` <sub><sup>→</sup></sub> `font-weight`
- `family` <sub><sup>→</sup></sub> `font-family`
- `size` <sub><sup>→</sup></sub> `font-size`
- `variant` <sub><sup>→</sup></sub> `font-variant`
- `kerning` <sub><sup>→</sup></sub> `font-kerning`
- `tracking` <sub><sup>→</sup></sub> `letter-spacing`
- `leading` <sub><sup>→</sup></sub> `line-height`
- `size-adjust` <sub><sup>→</sup></sub> `font-size-adjust`
- `style` <sub><sup>→</sup></sub> `font-style`
- `stretch` <sub><sup>→</sup></sub> `font-stretch`
- `feature-settings` <sub><sup>→</sup></sub> `font-feature-settings`

- `transform` <sub><sup>→</sup></sub> `text-transform`
- `shadow` <sub><sup>→</sup></sub> `text-shadow`
- `rendering` <sub><sup>→</sup></sub> `text-rendering`
- `underline-position` <sub><sup>→</sup></sub> `text-underline-position`
- `decoration` <sub><sup>→</sup></sub> `text-decoration`
- `decoration-line` <sub><sup>→</sup></sub> `text-decoration-line`
- `decoration-style` <sub><sup>→</sup></sub> `text-decoration-style`
- `decoration-color` <sub><sup>→</sup></sub> `text-decoration-color`

- `alternates` <sub><sup>→</sup></sub> `font-variant-alternates`
- `caps-variant` <sub><sup>→</sup></sub> `font-variant-caps`
- `east-asian-variant` <sub><sup>→</sup></sub> `font-variant-east-asian`
- `ligatures-variant` <sub><sup>→</sup></sub> `font-variant-ligatures`
- `numeral-variant` <sub><sup>→</sup></sub> `font-variant-numeric`
- `position-variant` <sub><sup>→</sup></sub> `font-variant-position`

### “@mixin”s

#### style

Include a full style:

```scss
body {
  @include font.style('body');
}
```

#### rule

Add a single rule:

```scss
body {
  @include font.rule('body', color);
}
```


### “@function”s

#### get-value

Get the value of a single rule:

```scss
body {
  color: font.get('body', color);
  font-size: font.get('body', size, 'px');
  font-size: font.get('body', size, 'rem');
}
```

When `get`ting `size` you may also pass `$unit` as a third parameter
to explicitly request either the `px` or `rem` values.
By default this will return in the same unit as `$length-unit`,
or `rem` if `$length-unit` is `rem-px`.


### FAQ

- [I get the error: Error: Can’t find stylesheet to import](#i-get-the-error-error-cant-find-stylesheet-to-import)
- [My version of SASS doesn’t have @use and I can’t upgrade](#my-version-of-sass-doesnt-have-use-and-i-cant-upgrade)

#### I get the error: Error: Can’t find stylesheet to import

If you have installed SASS Typography via npm or yarn you will
need to add `SASS_PATH=node_modules` to your call too sass.\
Something like: `SASS_PATH=node_modules sass app.scss app.css --watch`

Alternatively you can copy the `_t.scss` file into your own file directory.
Then you can `@use` that file directly.
However, this means you will need to do updates manually.

#### My version of SASS doesn’t have @use and I can’t upgrade

This should be fine, and should work as normal without the initial `@use`.
The only issue may be that you now have functions with less readable names.\
If this becomes an issue for many people I will look into making less clashy
aliases for mixins and functions.
