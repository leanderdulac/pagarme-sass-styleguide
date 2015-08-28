# pagarme-sass-styleguide
The awesome sass styleguide that we follow at Pagar.me

> "Adding more people to a team should improve the team’s performance. A process must be in place that ensures that new developers are brought up to speed quickly and are duly allocated their specific areas of responsibility. Code must be carefully structured to ensure its maintainability over time and through team changes."

# Table of Contents

  1. [Syntax and Formatting](#syntax-and-formatting)
    1. [Methodology](#methodology)
      1. [Block](#block)
      1. [Elements](#elements)
      1. [Modifier](#modifier)
    1. [CSS Ruleset](#css-ruleset)
    1. [Strings](#strings)
    1. [Numbers](#numbers)
    1. [Colors](#colors)
    1. [Lists](#lists)
    1. [Selectors](#selectors)
    1. [Variables](#variables)
    1. [Constants](#constants)
    1. [Nesting](#nesting)
    1. [Mixings](#mixings)
  1. [Structure](#structure)
    1. [Base](#base)
    1. [Layout](#layout)
    1. [Modules and Components](#modules-and-components)
    1. [Utilities](#utilities)
    1. [Shame](#shame)

# Syntax and Formatting

## Methodology

This styleguide assumes [BEM methodology](https://en.bem.info/) to provide modular organization, clear and self-explanatory names for style components.

### Block

It's name follows the block-name scheme and defines a namespace for elements and modifiers.

```html
<!-- Awesome HTML -->
<div class="news-feed"></div>
```

```scss
//Awesome SASS
.news-feed {
  //That's a block!
}
```

### Elements

The namespace defined by the name of a block identifies an element as belonging to the block. An element name is delimited by a double underscore `__`.

**Avoid** using elements within elements. It is not recommended by the BEM methodology.

```html
<!-- Awesome HTML -->
<div class="news-feed">
  <div class="news-feed__card"></div>
  <div class="news-feed__card"></div>
  <div class="news-feed__card"></div>
</div>
```

```scss
//Awesome SASS
.news-feed {

  &__card {
    //That's an element!
  }
}
```

### Modifier

The namespace defined by the name of a block identifies a modifier as belonging to that block or its element. A modifier name is delimited by two (2) hyphens `--`.

A modifier can belong to a **Block** or an **Element** and **must not** use it outside of the context of its owner.

The full name of a modifier is created using the scheme:

  * For Boolean modifiers — `.news-feed__card--mod-name`.
  * For key-value type modifiers — `.news-feed__card--mod-name--mod-val`.

```html
<!-- Awesome HTML -->
<div class="news-feed news-feed--friend news-feed--theme--greeny">
    <div class="news-feed__card"></div>
    <div class="news-feed__card news-feed__card--hidden"></div>
</div>
```

```scss
//Awesome SCSS
.news-feed { //Block

  &_friend {} //Boolean Block Modifier
  
  &--theme--greeny {} //Key-value Block Modifier
  
  &__card { //Element
    &--hidden {} //Boolean Element Modifier
  }
}
```

## CSS Ruleset

* Ideally, 80-characters wide lines
* One (1) tab for indentation
* One (1) space after `:`
* No spaces between property value and `;`
* One (1) space between selector and first `{`
* One (1) new line after first `{`
* One (1) css property per line
* One (1) new line after last property, last `}` should have its own line
* Related selectors on the same line; unrelated selectors on new lines;
* New line for nested stuff.
* `@include` statements always first

```scss
// Awesome
.news-feed {
  background: red;
  width: 100%;
  height: 40px;
  overflow: hidden;
  
  &--green {
    @include green-feed();
    border-radius: 6px;
  }
  
  &__button {
    width: 125px;
    height: 30px;
  }
}

.news-feed, .sidebar-news-feed, //Those are related selectors
.subscribe-button { //and .subscribe-button is not
  background: blue;
}

```


## Strings

Always use single quotes `'`.

To avoid any potential issue with character encoding, use UTF-8 encoding in the main stylesheet using the @charset directive. Make sure it is the very first element of the stylesheet and there is no character of any kind before it.

```scss
@charset 'utf-8';
```

## Numbers

* Numbers should display leading zeros before a decimal value less than one.
* **Never** display trailing zeros.
* When dealing with lengths, a 0 value should never ever have a unit.
* Always do calculations wrapped by parenthesis `()`

```scss
// Awesome
$news-feed-base-height: 400px;
.news-feed {
  padding: 2em;
  opacity: 0.5;
  top: 0;
  height: ($news-feed-base-height / 2);
}

// Nope, dude
.news-feed {
  padding: 2.0em;
  opacity: .5;
  top: 0px;
  height: $news-feed-base-height / 2;
}
```

## Colors

* Always prefer named colors over its hex value
* When using rgb, rgba or hsl color functions, use a space after each comma `,`

```scss
// Awesome
.foo {
  color: red;
  background: rgba(23, 54, 212, 0.5);
}

// Nope, dude
.foo {
  color: #FF0000;
  background: rgba(0,0,0,.5);
}
```

## Lists

Lists are the Sass equivalent of arrays. A list is a flat data structure (unlike maps) intended to store values of any type (including lists, leading to nested lists).

* Either inlined or multilines
* Necessarily on multilines if too long to fit on an 80-character line
* Unless used as is for CSS purposes, always comma separated
* Always wrapped in parenthesis
* Trailing comma if multilines, not if inlined

```scss
// Awesome
$font-stack: (Helvetica, Arial, sans-serif);

// Awesome
$font-stack: (
  Helvetica,
  Arial,
  sans-serif,
);

// Nope, dude
$font-stack: Helvetica Arial sans-serif;

// Nope, dude
$font-stack: Helvetica, Arial, sans-serif;

// Nope, dude
$font-stack: (Helvetica, Arial, sans-serif,);
```


## Selectors

* **Avoid** tag name selectors so unwanted styles will not persist
* Use classes for **everything**, ids should be restricted for javascript purposes only, such as testing or `getElementById()` method.
* Should be written in [kebab-case](https://en.wikipedia.org/wiki/Kebab_case)
 
```scss
//Awesome
.nice-class-name {
  // (...)
}
```
 
## Variables

* Should be written in [kebab-case](https://en.wikipedia.org/wiki/Kebab_case)
* Should have one space after `:` and no space between value and `;`
* Should have meaningful names so confusion can be avoided
* Nested variables should have one `_` per nesting level so you have a clear idea about the scope of the variable
 
```scss
//Awesome
$root-dashboard-red: #FF3212;

.first-level {
  $_first-level-dashboard-red: #FF1208;
  
  .second-level {
    $__second-level-dashboard-red: #FF2141;
  }
}
```

## Constants

As long as SASS does not have any support for contants, let's adopt a different naming strategy for it
* Should be written in [snake-case](https://en.wikipedia.org/wiki/Snake_case)
* Should have all characters set to **Uppercase**
* Should have meaningful names so confusion can be avoided
 
```scss
$DASHBOARD_ALLOWED_POSITIONS: (top, right, bottom, left);
$DASHBOARD_GRAY_BLACK: #484848;
```

## Nesting

Nesting is a powerful tool for organizing your code, but let's make some rules clear so it will not be misused.

* Always use `&` for referencing the current selector
* Always nest pseudo-elements and pseudo-classes such as `::after` or `:first-child`
* Always nest selector state such as `:hover`
* Always nest to follow BEM conventions using `&`
* Nesting should follow this order: CSS properties, pseudo-classes, pseudo-elements, modifiers and for last elements
* Never go deeper than 3 nesting levels and [here is why](http://www.sitepoint.com/beware-selector-nesting-sass/)

```scss
//Awesome
.foo-bar {
  background: red;
  
  &:hover {
    background: blue;
  }
  
  &--active {
    background: cadetblue;
  }
  
  &::after {
    content: '';
    display: table;
    clear: both;
  }
}
```

## Mixings

* Should be written in [kebab-case](https://en.wikipedia.org/wiki/Kebab_case)
* Should have meaningful names so confusion can be avoided
* Should be used to avoid repetitive code
* Should have the same format as the [CSS Ruleset](#css-ruleset) section
* If you expect an unlimited number of arguments, use an arglist. This data type has been designed for such a purpose.
* If you expect a limited number of arguments, use multiple named arguments. This will allow you to pass them one by one or all at once using a list or a map.
* If you expect a list for your mixin/function, use a list.
 
```scss
//Awesome
@mixing circle-shape($size) {
  width: $size;
  height: $size;
  border-radius: $size;
}
```

# Structure

To maintain the sass code organized and modularized this styleguide structure section is inspired in Atomic Design and SMACSS standards. The goal here is to abstract code that is re-used accross the application into specific files to avoid repetition and exponential growth of you style code.

Classes should be restricted to BEM conventions, so there should not be any class to dictate a particular style, a class should belong to a Block, Element or Modifier. Anything out of that scope should be extended and not placed within the HTML class attribute. The goal is to not make large classets and maintain class names semantic.

## Folder structure

```
| base/
| components/
| modules/
| pages/
| utilities/
| shame/
```

#### Base

Lowest level style code, such as normalize.css and reset.css and it is the only place that tag names should be stylized for application general purposes. Note that the layout folder was transformed into a layout file into this folder, so you can place all your layout classes here to extend them.

```
base/
  normalize.scss
  reset.scss
  base.scss
  layout.scss
```

#### Components

Components are the smallest pieces of your applications, such as inputs or buttons and they should be used to form a module.

```
components/
  dropdown.scss
  form-fields.scss
  buttons.scss
```

#### Modules

Modules are structures that should live by theirselves and not depend on any other style. It is the result of many components assigned together.

```
modules/
  navigation.scss
  form.scss
```

#### Pages

One file per page of you application, that should only contain everything that is particular of that page, everything that is not used in 2 or more places yet, should be here. If the same code exists in 2 or more page files at the same time, you should create a module or a component file for it.

```
pages/
  home.scss
  myaccount.scss
  products.scss
```

#### Utilities

Global Mixings and variables files should go here.

```
utilities/
  mixings.scss
  variables.scss
```

#### Shame

Hacky style code stuff for individual "browsers" goes here. Shame on you, IE!

```
shame/
  ie6.scss
  ie7.scss
  ie8.scss
```
