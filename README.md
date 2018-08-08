# Adaptable

**Adaptable** is a Sass (SCSS) mixins library for building flexbox based grids.

## Installation

With yarn:

```zsh
yarn add adaptable
```

With npm:

```zsh
npm install adaptable
```

Then just import **Adaptable** at the top of your main sass file.

If you setup `includePaths: ["./node_modules"]` in your Sass build task, you can use `@import "adaptable/core/adaptable";` to import the library into a sass file.

## Usage

### Settings

**Adaptable** is build around two configuration units in the form of sass maps, that can be overwritten depending on each project needs or grid requirements.

#### Adaptable grid

This variable is a sass map that overrides Adaptable's default grid settings. Use this to define your project's grid properties including gutters, total column count or grid debugging color.

_Default settings:_

```scss
$adaptable-grid: (
  columns: 12,
  // Total number of columns (unitless number)
    gutter: 24px,
  // Grid gutter width between columns (number with unit)
    color: rgba(#00d4ff, 0.25),
  // Grid debugging color
    (
      any valid color format
    )
);
```

#### Adaptable breakpoints

This variable is a sass map that overrides Adaptable's default breakpoints.

Adaptable is using [SassMQ](https://github.com/sass-mq/sass-mq) under the hood for handling breakpoints and therefore the default values are inherited from this library.

_Default settings:_

```scss
$adaptable-breakpoints: (
  mobile: 320px,
  tablet: 740px,
  desktop: 980px,
  wide: 1300px
);
```

_Example of custom settings:_

```scss
$adaptable-breakpoints: (
  small: 320px,
  medium: 640px,
  large: 960px
);
```

### Mixins

#### Grid container

Creates a grid container with flexbox properties.

##### Example

_SCSS_

```scss
.element {
  @include grid-container;
}
```

_CSS Output_

```css
.element {
  display: flex;
  flex-wrap: wrap;
}
```

#### Grid column

Creates a grid column of requested size.

##### Example

_SCSS_

```scss
.element {
  @include grid-column(3);
}
```

_CSS Output_

```css
.element {
  flex: 0 0 calc(25% - 30px);
  max-width: calc(25% - 30px);
  margin-left: 24px;
}
```

#### Grid span

Spans an element across the width of specified columns.
Similar to `grid-column` but without setting a margin-left. Useful for nested grids or when only the width of the element is desired for the output.

##### Example

_SCSS_

```scss
.element {
  @include grid-span(3);
}
```

_CSS Output_

```css
.element {
  flex: 0 0 calc(25% - 30px);
  max-width: calc(25% - 30px);
}
```

#### Grid nest

Creates a sub-grid object that consumes the gutters of its container, for use in nested layouts.

##### Example

_SCSS_

```scss
.element {
  @include grid-nest;
}
```

_CSS Output_

```css
.element {
  display: flex;
  flex-wrap: wrap;
  margin-left: -24px;
  margin-right: -24px;
  flex: 0 0 calc(100% + 48px);
  max-width: calc(100% + 48px);
}
```

#### Grid breakout

Creates negative left and right margins dictated by the specified number of columns.
Useful to break out of a smaller parent grid.

##### Example

_SCSS_

```scss
.element {
  @include grid-breakout(1 of 8);
}
```

_CSS Output_

```css
.element {
  margin-right: calc(-12.5% - 1.6875rem + 1.5rem);
  margin-left: calc(-12.5% - 1.6875rem + 1.5rem);
}
```

#### Grid push

Push or pull a grid column by manipulating its left margin.

##### Example

_SCSS_

```scss
.element {
  @include grid-push(3);
}
```

_CSS Output_

```css
.element {
  margin-left: calc(25% - 30px + 48px);
}
```

#### Grid shift

Shift columns and reorder them within their container using relative positioning.

##### Example

_SCSS_

```scss
.element {
  @include grid-shift(3);
}
```

_CSS Output_

```css
.element {
  position: relative;
  left: calc(25% - 30px + 24px);
}
```

#### Grid media

`grid-media` allows you to change your layout based on a media query.
For example, an object can span 3 columns on small screens and 6 columns
on large screens.

This mixin is a wrapper around SassMQ's [mq](https://github.com/sass-mq/sass-mq/blob/master/_mq.scss#L121) mixin.

##### Example

_SCSS_

```scss
.element {
  @include grid-media($from: mobile) {
    color: red;
  }
  @include grid-media($until: tablet) {
    color: blue;
  }
  @include grid-media(tablet, desktop) {
    color: green;
  }
}
```

_CSS Output_

```css
@media (min-width: 20em) {
  .element {
    color: red;
  }
}

@media (max-width: 46.24em) {
  .element {
    color: blue;
  }
}

@media (min-width: 46.25em) and (max-width: 61.24em) {
  .element {
    color: green;
  }
}
```

#### Grid debug

Creates a series of guide lines using the `background-image` property on a grid container to visualise the columns and gutters of the grid.

##### Example

_SCSS_

```scss
.element {
  @include grid-debug;
}
```

_CSS Output_

```css
.element {
  background-image: repeating-linear-gradient(…);
}
```

## Contributing

See the [contributing](./CONTRIBUTING.md) documentation.

## Credits

**Adaptable** is an opinionated customised fork of Thoughtbot's [Neat](https://github.com/thoughtbot/neat) library.
