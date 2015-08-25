# pagarme-sass-styleguide
The awesome sass styleguide that we follow at Pagar.me

> "Adding more people to a team should improve the team’s performance. A process must be in place that ensures that new developers are brought up to speed quickly and are duly allocated their specific areas of responsibility. Code must be carefully structured to ensure its maintainability over time and through team changes."

## Table of Contents

  1. Syntax and Formatting
    1. [Methodology](#methodology)
      1. [Block](#block)
      1. [Elements](#elements)
      1. [Modifier](#modifier)
    1. [CSS Ruleset](#css-ruleset)
    1. [Selectors](#selectors)
    1. [Variables](#variables)
    1. [Constants](#constants)
    1. [Nesting](#nesting)
    1. [Mixings](#mixings)
  1. Structure

## Methodology

This styleguide assumes [BEM methodology](https://en.bem.info/) to provide modular organization, clear and self-explanatory names for style components.

### Block

* The name should reference a block namespace

### Elements

### Modifier

## CSS Ruleset

* Ideally, 80-characters wide lines
* One (1) tab for indentation
* One (1) space after `:`
* No spaces between property value and `;`
* One (1) space between selector and first `{`
* One (1) new line after first `{`
* One (1) new line after last property, last `}` should have its own line
* Related selectors on the same line; unrelated selectors on new lines;
* New line for nested selectors.
* `@include` statements always first

```scss
// Awesome
.foo-bar {
  background: red;
  width: 100%;
  height: 40px;
  overflow: hidden;
  
  &.green {
    background: green;
  }
  
  .foo-bar-button {
    border-radius: 4px;
  }
}

.foo, .foo-bar,
.circle {
  @include awesomeness();
  background: blue;
}

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
* Always nest pseudo-classes and pseudo-elements such as `::after` or `:first-child`
* Always nest selector state such as `:hover`
* Always nest selectors that dictate current selector variations, for instance `.is-active`
* Never go deeper than 3 nesting levels, and [here is why](http://www.sitepoint.com/beware-selector-nesting-sass/)

```scss
//Awesome
.foo-bar {
  background: red;
  
  &:hover {
    background: blue;
  }
  
  &.active {
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
@mixing create-circle($size) {
  width: $size;
  height: $size;
  border-radius: $size;
}
```
