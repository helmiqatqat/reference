# SASS

|Table of Contents|
|-----------------|
|[Introduction](#introduction)|
|[Import and Use](#import-and-use)
|[Project Structure](#project-structure)|
|[Nesting & Parent Element](#nesting--parent-element)
|[Property Declaration & Placeholder](#property-declaration--placeholder)
|[Control flow - If and Else](#control-flow---if-and-else)
|[Interpolation](#introduction)
|[Comments](#comments)
|[Mixin and Include](#mixin-and-include)
|[Loops](#loops)
|[SASS Built-in functions](#sass-built-in-functions)
|[Functions](#functions)

## Introduction

### What is Sass

- Sass stands for Syntactically Awesome Stylesheet
- Sass is an extension to CSS
- Sass is a CSS pre-processor
- Sass is completely compatible with all versions of CSS
- Sass reduces repetition of CSS and therefore saves time
- Sass was designed by Hampton Catlin and developed by Natalie Weizenbaum in 2006
- Sass is free to download and use.

### Why Use Sass

Stylesheets are getting larger, more complex, and harder to maintain. This is where a CSS pre-processor can help.

Sass lets you use features that do not exist in CSS, like variables, nested rules, mixins, imports, inheritance, built-in functions, and other stuff.

### How Does Sass Work

A browser does not understand Sass code. Therefore, you will need a Sass pre-processor to convert Sass code into standard CSS.

This process is called transpiling. So, you need to give a transpiler (some kind of program) some Sass code and then get some CSS code back.

## Import and Use

To import code from a file we simply write down:

```SCSS
@import 'file_name.scss' 
```

In newer versions of SASS import can still be used, however it is replaced with @use as follows:

```SCSS
@use 'file_name.scss'
```

## Project Structure

Writing scss in separate files can make code easier to understand and more reusable and easy to maintain. We write the scss files that partials of the main scss file by adding underscore before the file name, and that tells the main scss file that these are partial files.

```bash
index.scss
functions
  _functions.scss
variables
  _variables.scss
normalize
  _normalizer.scss
components
  _components.scss
utilities
  _utilities.scss
```

## Variables

To write variables in SASS we simply use dollar sign $ and write the variable name as follows:

```SCSS
$primary_color: red;

.container {
  color: $primary_color
}
```

How ever example above showed global variable, we can make a local variable to be only used inside its class as follows:

```SCSS
.container {
  $primary_color: red;
  color: $primary_color
}
```

We can edit the global variable of the same name of local variable by adding '!global' flag to the right of the local variable,

```SCSS
$primary_color: red;
.text {
  color: $primary_color
}
.container {
  $primary_color: orange !global;
  color: $primary_color
}
.card {
  color: $primary_color
}
```

Now the element of class _text_ will have a **red** color, the element of class _container_ will have **orange** color, but the element of class _card_ will have the **orange** color because the variable is adjusted to orange, just in like javascript and css it is excuted line by line so the element of class _text_ when have been read, the variable had the value of **red**, then it got changed to **orange** before excuting the _card_ class.

## Nesting & Parent Element

So in _CSS_ when we want to nest elements we use the following format:

```CSS
.parent{
  color: red;
}
.parent > .child {
  color: green;
}
.parent .child .grand-child {
  color: blue;
}
```

How ever in _SASS_ it is less repeatative, the same code above will be written as follows:

```SCSS
.parent {
  color: red;
  .child {
    color: green;
    .grand-child{
      color: blue;
    }
  }
}
```

### Selectors

```SCSS
.parent > {
  color: red;
  .child {
    color: green;
  }
}
// In CSS this is equivalent to:
.parent {
  color: red;
}
.parent > .child {
  color: green;
}
```

### Parent multiple class names

If the parent element has a class name lets say container, and it also has other classes, as in light and dark mode it will be different in color and background color so can write inside the curly brackets the ampersand symbol **&** and then the class name as follows:

```SCSS
.parent {
  &.light-mode {
    color: black;
    background-color: white;
  }
  &.dark-mode {
    color: white;
    background-color: black;
  }
  &:hover {
    cursor: pointer;
  }
  [dir="rtl"] & {
    direction: rtl
  }
}
// In CSS this is equivalent to:
.parent.light-mode {
  color: black;
  background-color: white;
}
.parent.dark-mode {
  color: black;
  background-color: white;
}
.parent:hover {
    cursor: pointer;
}
[dir="rtl"] .box {
  direction: rtl
}
```

## Property Declaration & Placeholder

### Property Declaration

If we want write a main property that has multiple sub properties, we can achieve this as follows:

```SCSS
.parent{
  font: {
    size: 12px;
    weight: bold;
  }
  margin: auto {
    top: 12px;
    bottom: 20px;
  }
}
// In CSS this is equivalent to:
.parent {
  font-size: 12px;
  font-weight: bold;
}
```

### Place Holder

If we have multiple classes that share the same properties of one of the classes we can abstract the properties from that class and use it in other classes and we can achieve this by adding **@extends class_name**

```SCSS
.main {
  font-size: 18px;
  color: #999;
  background-color: #333
}
.article {
  @extend .main;
  padding: 20px;
}
.sidebar {
  margin: 20px;
  @extend .main;
  padding: 10px;
}
// In CSS this is equivalent to:
.main, .article, .sidebar {
  font-size: 18px;
  color: #999;
  background-color: #333
}
.article {
  padding: 20px;
}
.sidebar {
  margin: 20px;
  padding: 10px;
}
```

If we dont have a class name called _main_ and we just want to make it a **placeholder** for multiple shared properties we simply write the precent symbol '%' then the name _main_ as seen in the example below:

```SCSS
%main {
  font-size: 18px;
  color: #999;
  background-color: #333
}
.article {
  @extend %main;
  padding: 20px;
}
.sidebar {
  margin: 20px;
  @extend %main;
  padding: 10px;
}
// In CSS this is equivalent to:
.article, .sidebar {
  font-size: 18px;
  color: #999;
  background-color: #333
}
.article {
  padding: 20px;
}
.sidebar {
  margin: 20px;
  padding: 10px;
}
```

## Control flow - If and Else

```SCSS
$theme: 'light';
.page {
  @if $theme == 'light' {
    background-color: white;
    color: black;
  }
  @else {
    background-color: black;
    color: white;
  }
}
$rounded: true;
.box {
  border-radius: if($rounded, 5px, null)
}
```

### Operators

To do conditions we need to have operators, the operators in sass is written as follows:

#### Numerical Operators

- **==**: equals.
- **!=**: does not equal.
- **>**: bigger than.
- **>=**: bigger than or equal.
- **<**: smaller than.
- **<=**: smaller than or equal.

#### Logical Operators

- **and**: when want all conditions to be true to apply a specific styling.
- **or**: when we want one of the conditions to be true to apply a specific styling.

## Interpolation

To write variables names inside a class name we simply add ```#{$variable_name}``` as follows:

```SCSS
$school: "root-academy"
$logo-position: "left"
.#{$school}-school {
  background-image: url('./images/#{$school}.png')
  #{$logo-position}: 0;
}
// In CSS this is equivalent to:
.root-academy-school {
  background-image: url('./images/root-academy.png');
  left: 0px;
}
```

## Comments

Comments can contain variables throught interpolation as follows:

```SCSS
$author: "Helmi"
/* This comment is created by #${author} */

// In CSS this is equivalent to:
/* This comment is created by Helmi */
```

### Comments that does not appear in css file

```SCSS
// This comment will not appear in css file
```

### Comments that appears in css file but no in compressed version

```SCSS
/* This comment will appear in css file but not in compressed version */
```

### Comments that appears in css file and the compressed version as well

```SCSS
/*! This comment will appear in css file and in compressed version as well*/
```

### Comments that are used for documentation

```SCSS
/// This comment is used for documentation
```

## Mixin and Include

Now mixin is kind of similar to the placeholder, however each have their own use cases. Mixin is more like a function class where parameters determine the properties of the class.

```SCSS
@mixin list {
  padding: 0;
  margin: 0;
  text-decoration: none;
}
ul {
  @include list;
}
@mixin circle($dimensions) {
  border-radius: 50%
  width: $dimensions;
  height: $dimensions;
}
.circle-100 {
  @include circle(100px);
  background-color: red;
}
```

### Content

Sometimes we want to write the properties ourselfs, inorder to do that we add ```@content``` inside the mixin function.

```SCSS
@mixin keyF($animation-name) {
  @-webkit-keyframes #{$animation-name} {
    @content;
  };
  @-moz-keyframes #{$animation-name} {
    @content;
  };
  @keyframes #{$animation-name} {
    @content;
  }
};

@include keyF(rotate) {
  from {
    transform: rotate(0deg)
  }
  to {
    transform: rotate(360deg)
  }
}
```

## Loops

### For

For loop in SASS is similar to the loop in javascript, however if we want to include the **<** and **<=** to specify weither we want to include the last index or not we use **to** that works as **<** and through that works as **<=**

```SCSS
@for $i from 1 to 3 {
} // result 1, 2

@for $i from 1 through 3 {
} // result: 1, 2, 3
```

### Each

#### Single Value

```SCSS
$themes: red, green, blue;
@each $theme in $themes {
  .#{$theme}-theme {
    border: 2px solid $theme;
  }
}
// In CSS this is equivalent to:
.red-theme {
  border: 2px solid red;
}
.green-theme {
  border: 2px solid green;
}
.blue-theme {
  border: 2px solid blue;
}
```

#### Multiple values

##### Object like variable

In case the variable has a key and value just like object:

```SCSS
$social-media: (
  "facebook": blue,
  "youtube": red,
  "github": black
);
@each $name, $color in $social-media {
  .#{$name} {
    background-color: $color
  }
}
// In CSS this is equivalent to:
.facebook {
  background-color: blue;
}
.youtube {
  background-color: red;
}
.github {
  background-color: black;
}
```

##### Destructuring

```SCSS
$classes: 'one' 20px red, 'two' 10px green, 'three' 15px blue;
@each $class, $font, $color in $classes {
  .#{#class} {
    font-size: $font;
    color: $color;
  }
}
// In CSS this is equivalent to:
.one {
  font-size: 20px;
  color: red;
}
.two {
  font-size: 10px;
  color: green;
}
.three {
  font-size: 15px;
  color: blue;
}
```

### While

The syntax in while loop is as follows:

```SCSS
$count: 1; 
@while $count <= {
  ...
  $count: $count + 1;
}
```

## SASS Built-in functions

- unique-id(): is used to generate random unique id consists of digits and characters.

- percentage(): is used to get the percentage from dividing one number on another.

## Functions

The syntax for writing functions is, and an example of calling it:

```SCSS
@function half($size) {
  @return $size / 2;
}

$width: 200px;
.element {
  width: $width;
  height: half($width);
}

// In CSS this is equivalent to:
.element {
  width: 200px;
  height: 100px;
}
```

In case we do not know how many times our parameters there will be in our function we use rest parameters as follows:

```SCSS
@function calculateSum($values...) {
  $sum: 0;
  @each $value in $values {
    $sum: $sum + $value
  }
  @return $sum
}
```
