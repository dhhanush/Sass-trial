# Sass Trials

- sass variables - these variables are compiled to actual values and unlike the css variables.

## css variables

```scss
:root{
--primary-color: blue;
}

body{
    background-color: var(--primary-color);
}

---
-scss variables
---

$primary-color: red;

body{
    background-color: $primary-color;
}
```

## Maps

```scss
$font-weights: (
  'regular': 400,
  'medium': 600,
  'bold': 900,
);

font-weight: map-get($font-weights, 'bold');
```

## Nesting

```html
<div class="main">
  <p class="main__paragraph">Hi there, How are you doing?</p>
</div>
```

```scss
.main {
  width: 80%;
  margin: 0 auto;

  p {
    color: white;
  }
}

or .main {
  width: 80%;
  margin: 0 auto;

  #{&}__paragraph {
    // this is interpolation
    color: white;

    &:hover {
      color: pink;
    }
  }
}
```

## Partials

```scss
//_partials.scss
//@import "config", "main", "home", "menu", "about", etc; - way to import multiple partials

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

//to include
@import './partials'; //in the main and we don't have to use underscore or extensions
```

## Functions

```scss
@function weight($weight-name) {
  @return map-get($font-weights, $weight-name);
}

//to use

.main {
  font-weight: weight(bold);
}
```

## Mixins

```scss
@mixin flexcenter {
  display: flex;
  justify-content: center;
  align-items: center;
}

//to use the mixins
.main {
  @include flexcenter;
}
```

### Mixin with params

```scss
@mixin flexcenter($flex-direction) {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: $flex-direction;
}

//to use the mixins
.main {
  @include flexcenter(row);
}
```

functions and mixins are similar but functions should be used to compute or return values and mixins are used to define styles

### choosing between light and dark theme using mixins

```scss
@mixin theme($light-theme: true) {
  @if $light-theme {
    background-color: lighten($primary-color, 100%);
    color: darken($text-color, 100%);
  }
}

//to use the mixins
.light {
  @include theme(false);
}
```

### mixins for media-queries

```scss
@mixin mobile {
  @media (max-width: 800px) {
    @content;
  }
}

//to use the mixins
.main {
  @include mobile {
    flex-direction: 'column';
  }
}
```

## Extend

```scss
// we can extend class properties using the extend key

.main {
  #{&}__paragraph1 {
    font-weight: bold;

    &:hover {
      color: pink;
    }
  }

  #{&}__paragraph2 {
    @extend .main__paragraph1;

    &:hover {
      color: blue;
    }
  }
}
```

## Mathematical operations

```scss
// with normal css calculations we use calc function to do the calculation like calc(80% - 40%), but in scss we dont have to use calc functions

.main {
  width: 80% - 40%;
}

//but the catch is in css calc function we can mix types , like we can calc(80% - 400px) , but in scss we can't mix types
```
