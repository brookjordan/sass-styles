# SASS Styles — Containers

Define container styles once, use everywhere

## Installation

```
npm install sass-styles-containers
```

## Usage

As early as possible, include:
```scss
// entry.scss
@use "my-containers" as my-containers;
@use "sass-styles-containers" with (
  $styles: my-containers.$styles,
);

@use "base";
```
```scss
// _base.scss
@use "sass-styles-containers" as c;
body {
  @include c.style(body);
}
```
```scss
// _my-containers.scss
$styles: (/* rule definitions */);
```

Note: Output is *HIGHLY* unoptimised. As such you should include a good CSS minifier as part of your build.

An example of the cleanup provided by [CSS Nano](https://cssnano.co):
```scss
/* Styles */
$styles: (
  warning-outline: (
    border-width: 5,
    border-style: solid,
    border-color: orange,
  ),
);

/* Usage */
@use "sass-styles-containers" as c;
.card {
  &--warning {
    @include c.style(warning-outline);
  }
}

/* Original output */
.card--warning {
  border-top-width: 5px;
  border-right-width: 5px;
  border-bottom-width: 5px;
  border-left-width: 5px;
  border-top-style: solid;
  border-right-style: solid;
  border-bottom-style: solid;
  border-left-style: solid;
  border-top-color: orange;
  border-right-color: orange;
  border-bottom-color: orange;
  border-left-color: orange;
}

/* After CSS Nano */
.card--warning{border:5px solid orange}
```


## Options

### $root-font-px-size

A Number

### $length-unit

`px`, `rem`, or `rem-px`

Note: whichever unit is chosen,
unitless length values are assumed to be in `px`.

### $styles


## “@mixin”s

### print

### print-rule


## FAQ

- [noop](#no-op)

### No op

No operation
