# vue-clickaway2

> Reusable clickaway directive for reusable [Vue.js](https://github.com/vuejs/vue) components

[![npm version](https://img.shields.io/npm/v/vue-clickaway2.svg)](https://www.npmjs.com/package/vue-clickaway2)

## Overview

Sometimes you need to detect clicks **outside** of the element (to close a modal
window or hide a dropdown select). There is no native event for that, and Vue.js
does not cover you either. This is why `vue-clickaway2` exists. Please check out
the [demo](https://jsfiddle.net/simplesmiler/4w1cs8u3/150/) before reading further.

Vue-Clickaway2 is a continuation of [Vue-Cickaway](https://www.npmjs.com/package/vue-clickaway).

## Requirements

- vue: ^2.0.0

If you need a version for Vue 1, try `vue-clickaway@1.0`.

## Install

From npm:

``` sh
$ npm install vue-clickaway2 --save
```

## Usage

1. Make the directive available to your component
2. Define a method to be called
3. Use the directive in the template

The recommended way is to use the mixin:

``` js
import { mixin as clickaway } from 'vue-clickaway2';

export default {
  mixins: [ clickaway ],
  template: '<p v-on-clickaway="away">Click away</p>',
  methods: {
    away: function() {
      console.log('clicked away');
    },
  },
};
```

If mixin does not suit your needs, you can use the directive directly:

``` js
import { directive as onClickaway } from 'vue-clickaway2';

export default {
  directives: {
    onClickaway: onClickaway,
  },
  template: '<p v-on-clickaway="away">Click away</p>',
  methods: {
    away: function() {
      console.log('clicked away');
    },
  },
};
```

You can pass an argument conataining any [HTML DOM Event](https://www.w3schools.com/jsref/dom_obj_event.asp) on the directive in the markup:

``` html
<p v-on-clickaway:mousedown="away">Click away</p>
<!-- If you don't pass an argument it'll default to click just like previous versions -->
```

## Caveats

1. Pay attention to the letter case. `onClickaway` turns into `v-on-clickaway`,
   while `onClickAway` turns into `v-on-click-away`.
2. Prior to `vue@^2.0`, directive were able to accept statements.
   This is no longer the case. If you need to pass arguments, just do
   `v-on-clickaway="() => away(arg1)"`.
3. There is a common issue with dropdowns (and modals) inside an element with
   `v-on-clickaway`. Some UI libraries chose to implement these UI elements
   by attaching the DOM element directly to the body. This makes clicks on
   a dropped element trigger away handler. To combat that, you have to add
   an extra check in the handler, for where the event originated from.
   See #9 for an example.

## License

[MIT](https://opensource.org/licenses/MIT)
