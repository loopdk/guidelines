# ITK Design - CSS guidelines

This document is a CSS guidelines for working with projects at ITK Design.

These are *guidelines*, and if you think it's necessary to deviate feel free to do so, **but** please [be sensible](http://csswizardry.com/2010/08/semantics-and-sensibility/) and do this only because it's necessary.


* Be familiar with [SCSS](http://sass-lang.com/)
* Read [this](http://www.jakobloekkemadsen.com/2013/07/css-abstractions-done-right/)
* [And this about test driven CSS](http://www.jakobloekkemadsen.com/2012/09/tdcss-js/)
* Use [SCSS](http://sass-lang.com), but only [nest one level](exceptions-and-deviations)
* [Be sensible](http://csswizardry.com/2010/08/semantics-and-sensibility/)
* [Don't break the windows](http://en.wikipedia.org/wiki/Broken_windows_theory)
* [DRY](http://en.wikipedia.org/wiki/Don%27t_repeat_yourself)

## Content

1. [Comments](#comments)
2. [Declaration order](#declaration-order)
3. [Media queries](media-queries)


<a name="comments"></a>
## Comments

* Place comments on a new line above the subject

```css
/**
 * File name
 *
 * Optional description
 *
 * @author author name
 */ 


/* Section comment
 *
 * Optional description
 *
 * ========================================================================== */
   

/* This is an inline comment */
```

<a name="declaration-order"></a>
## 2. Declaration order

* One selector per line
* Add a single space after the colon of the declaration
* @extend goes in the top so we know if the ruleset inherits another
* Normal rules goes next
* @inlude goes

* Use predefined variables

```css
.class {
  @extend %placeholder();

  /* Positioning */
  position: absolute;
  z-index: 10;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;  
  

  /* Display & Box Model */
  display: inline-block;
  overflow: hidden;
  width: 100px;
  height: 100px;
  padding: 10px;
  border: 10px solid #333;
  margin: 10px;
  
  /* Other */
  background: $color;
  color: $white;
  font-family: $font-family;
  font-size: $font-size;
  text-align: right;
  
  @include mixin();
}
```

<a name="media-queries"></a>
## 3. Media queries

* Add media queries @includes after other @includes and @extends

```css
.class {  
  background-color: $blue;

  @include breakpoint-1() {
  	background-color: $red;
  }
  
  @include breakpoint-2() {
  	background-color: $red;
  }
}
```

<a name="exceptions-and-deviations"></a>
## 4. Exceptions and deviations

* You can nest two levels when using pseudo classes
* You can nest two levels when using media queries mixins
* If you have to deviate from the one limit nesting rule (except mentioned in this section), explain why in an inline comment