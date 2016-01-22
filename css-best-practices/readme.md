# CSS Best Practices


## Table of Contents

* [Code like it's 2020](#code-like-its-2020)
* [Selector specificity](#selector-specificity)
    * [Dos](#dos)
    * [Do nots](#do-nots)
* [A note on attribute selectors](#a-note-on-attribute-selectors)
* [Class naming convention](#class-naming-convention)
* [Self documenting selectors](#self-documenting-selectors)
* [Single direction rule](#single-direction-rule)
* [Name spacing](#name-spacing)
* [Size units](#size-units)
* [Context sensitivity](#context-sensitivity)
* [Format](#format)
* [Declaration order](#declaration-order)
    * [Exceptions and variations](#exceptions-and-variations)


## Code like it's 2020

Because we use Autoprefixer, we are able to write our code as if all our properties are fully supported. When compiled, Autoprefixer will of course convert any properties that have special requirements as far as compatibility is concerned and add prefixes to them as needed.

That includes things like Flexbox, CSS3 properties, and many more! This also means that we *should not* be using mixins for prefixing. Remember that Autoprefixer uses data from caniuse.com to determine what will be output — so properties that don't have enough browser support should probably still be avoided (or at least used with extreme caution).


## Selector specificity

We strive to write performant, portable, selectors whenever possible. In short, [keep your CSS selectors short](http://csswizardry.com/2012/05/keep-your-css-selectors-short/).

To help do that, it might be helpful to know how to measure specificity which [Smashing Magazine has an article just for that](http://www.smashingmagazine.com/2007/07/27/css-specificity-things-you-should-know/)!

### Dos:

* Use class names for specificity because it improves performance.
* Use the component oriented naming conventions outlined below.
* If you have no other choice and you must select an ID, use the attribute selector instead

### Do nots:

* Avoid using IDs. They decrease portability.
* Avoid using tag selectors. They both impact performance and portability.
* Never over qualify selectors because it impacts performance.

```scss
// NO
ul.button-group li.button {
}

// Yes
.button-group__button {
}

// NO
#something {
}

// Yes (Only as a last resort!)
[id="something"] {
}
```


## A note on attribute selectors

A common use case is to target input types. For example `input[type="text"]`.

It's important to realize that the element selector is not necessary here. If you think about it, we are actually increasing the specificity needlessly. Attribute selectors have the same specificity as a class. The above example has the same specificity as `input.someClass`

All we really need is `[type="text"]`, because that is sufficient for targeting text inputs.

In summary: *attribute selectors should be used alone*, just like classes.


## Class naming convention

We use BEM to name our components. It looks something like this:

```
.ui-component
.ui-component__sub-component
.ui-component--modifier
```

We cover this convention in greater detail [here](../class-naming-conventions#class-naming-conventions).


## Size Units

* Use pixels for fixed-width elements.
* Use percentages for fluid-width elements.
* Use pixels for font-size because it offers absolute control over text.
* Use unitless line-height in conjunction with font-size because it acts as a multiplier of the pixel value.


## Context sensitivity

There are certain types of styles that are context sensitive, but tend to be written with no regard to that context. As an example, `absolute` positioning:

```
// Action bar
// ===

.action-bar {
  position: absolute;
  bottom: 0;
}
```

This is difficult to maintain because this CSS does not communicate anything about what's happening. What is this class absolutely positioned relative to? Good luck trying to figure that out, because chances are you're going to have to manually load up the page that this component exists on and inspect it to find it. That's assuming you know what page this component is used.

A better approach is to build code that is contextual aware. For example:

```
// PDP
// ===

// ...


// PDP: Summary
// ---
//
// 1. Absolutely position the action bar relative to the PDP Summary section

.pdp__summary {
  position: relative; // 1

  .action-bar {
    position: absolute; // 1
    bottom: 0;
  }
}
```

Not only is the code written in a way that clearly informs a reader how these context sensitive styles relate, we use documentation to make it perfectly explicit. There is no ambiguity here.

Another benefit is that this keeps our code isolated really well. Action Bar can be put anywhere and still work.


## Format

We want our CSS to be written consistently no matter who the code author is. In order to do so, please follow these below rules.

Note that we use [SCSS-Lint](https://github.com/causes/scss-lint) to make this easier — see our linting rules [here](https://github.com/mobify/mobify-code-style/blob/update-css-style/css/.scss-lint.yml).

* One selector per line
* Use a soft indent of two spaces
* Use one space between selector and first brackets
* Use one space between property and value after :
* Always add a semicolon after property value
* Use single quotes
* Do not specify units for a zero value (unless settings flex-basis because of an IE bug)
* Include a space after each comma in a comma separated property list
* User lowercase and shorthand hex values, e.g., #aaa
* Always use hex values unless you are declaring rgba.
* Separate each ruleset by an empty line
* Separate each declaration block by an empty line
* Use `//` for comment blocks (instead of `/* */`)

```scss
.selector1,
.selector2 {
  // This is a comment
  display: block;
  margin: 0 auto;

  background: #bada55 url('icon.png') center no-repeat;
}

.selector-a,
.selector-b {
    padding: 10px;

    background: rgba(255, 255, 255, 0.25);
}
```


## Declaration order

Following our practice of writing consistent code, we also want all properties to be consistently ordered according to the bellow standard.

And as before, we use [SCSS-Lint](https://github.com/causes/scss-lint) to help ensure property order is consistent - see our linting rules [here](https://github.com/mobify/mobify-code-style/blob/update-css-style/css/.scss-lint.yml).

1. Extends
1. Mixins/Includes (except for property specific mixins)
1. Position
1. Display & Box Model
1. Visual Styles
1. Text Styles
1. Vendor Prefixed Styles
1. Animations & Transitions
1. Pseudo-classes
1. Pseudo-elements
1. Modifier elements
1. Child elements

```scss
.c-selector {
    // Extends
    @extend %x-extend;

    // Includes
    @include mixin();

    // Content
    content: '\25B6';

    // Positioning
    position: absolute;
    left: 10px;
    z-index: 10;

    // Display & Box Model
    display: inline-block;
    overflow: hidden;
    box-sizing: border-box;
    width: 100px;
    height: 100px;
    margin: 10px;
    padding: 10px;
    border: 1px solid #333;

    // Visual styles
    background: #000;
    border-radius: 10px;
    @include box-shadow(5px 5px 0 rgba(0, 0, 0, 0);

    // Text styles
    color: #fff;
    font-family: sans-serif;
    font-size: 16px;
    text-align: right;

    // Vendor prefixed styles
    -webkit-user-select: none;
    -webkit-tap-highlight: rgba(0, 0, 0, 0);

    // Styles that don't fall under any of the above categories
    pointer-events: none;

    // Animations & Transitions
    transition: all 0.2s;

    // Pseudo-classes
    &:active {
        background: blue;
    }
    &:last-child {
        border-top: 1px solid blue;
    }

    // Pseudo-elements
    &::before {
        content: 'CSS Rules!';
    }

    // Modifier Elements
    &.x--light {
        background: #999;
    }

    // Child Elements
    span {
        font-weight: bold;
    }
}
```


### Exceptions and variations

Sometimes we break out of this convention to add to the readability of our stylesheets. This occurs especially often with long comma separated property values like gradients, shadows, transitions, or includes. These can be arrange across multiple lines and indentation levels to help with diffs and readability.

```scss
.x-selector {
    @include icon(
        home,
        $color: blue,
        $size: 15px
    );

    transition:
        opacity 0.2s ease-in-out,
        width 0.5s linear;
}
```

Continue on to [Sass (SCSS) Best Practices →](../sass-best-practices#sass-scss-best-practices)
