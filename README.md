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

Then just import `@import "adaptable/core/adaptable";` at the top of your main sass file.

**Note:** your Sass configuration **must** be set to access certain dependencies or installation will fail. Either:

- include [Eyeglass](https://github.com/sass-eyeglass/eyeglass) in your [build tools](https://github.com/sass-eyeglass/eyeglass#building-sass-files-with-eyeglass-support), or;
- set `node_modules` in your `includePaths`.

## Usage

### Settings

**Adaptable** is build around two configuration units in the form of sass maps, that can be overwritten depending on each project needs or grid requirements.

#### `$adaptable-grid`

This variable is a sass map that overrides Adaptable's default grid settings. Use this to define your project's grid properties including gutters, total column count or grid debugging color.

_Default settings:_

```scss
$adaptable-grid: (
  columns: 12,
  gutter: 24px,
  color: rgba(#00d4ff, 0.25),
);
```

##### Properties

| Name    | Type               | Default             | Description                                |
| ------- | ------------------ | ------------------- | ------------------------------------------ |
| columns | number (unitless)  | 12                  | Default number of the total grid columns.  |
| gutter  | number (with unit) | 24px                | Default grid gutter width between columns. |
| color   | HEX, RGBA          | rgba(#00d4ff, 0.25) | Default grid debug color.                  |

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
  flex: 1 0 calc(100% + 48px);
  flex-wrap: wrap;
  margin-left: -24px;
  margin-right: -24px;
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
  flex-shrink: 0;
  width: calc(25% - 30px);
  max-width: calc(100% - 48px);
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
  flex: 0 0 auto;
  width: calc(25% - 30px);
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
