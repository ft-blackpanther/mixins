# Mixins

![vue mixin image](https://i.imgur.com/rspToHb.jpg)

## What are Mixins?
Mixins in Vue JS are basically a chunk of defined logic, stored in a particular prescribed way by Vue, which can be re-used over and over to add functionality to your Vue instances and components. So Vue mixins can be shared between multiple Vue components without the need to repeat code blocks.

> Mixins are a flexible way to distribute reusable functionalities for Vue components. A mixin object can contain any component options. When a component uses a mixin, all options in the mixin will be “mixed” into the component’s own options.

Example:
```sh
// define a mixin object
var myMixin = {
  created: function () {
    this.hello()
  },
  methods: {
    hello: function () {
      console.log('hello from mixin!')
    }
  }
}

// define a component that uses this mixin
var Component = Vue.extend({
  mixins: [myMixin]
})

var component = new Component() // => "hello from mixin!"
```

[![Edit JSX - Element: React.createElement](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/modest-hodgkin-yhh7p)

## Types of Mixins
There are two types of mixins in Vue:
1. **Local Mixins:** It is scoped to the component it is imported into and registered in. The powers of the local mixin is bound by the component it is imported in.
2. **Global Mixins:** This is a different type of mixin that is defined in the main.js file of any Vue project. It affects all Vue components in an application so the Vue team advises that it be used with caution. A definition of a global mixin looks like this:
```sh
// main.js

Vue.mixin({
  mounted() {
    console.log("hello world!");
  }
});
```

## Option Merging
When a mixin and the component itself contain overlapping options, they will be “merged” using appropriate strategies.

For example, data objects undergo a recursive merge, with the component’s data taking priority in cases of conflicts.
 
```sh
var mixin = {
  data: function () {
    return {
      message: 'hello',
      foo: 'abc'
    }
  }
};

new Vue({
  mixins: [mixin],
  data: function () {
    return {
      message: 'goodbye',
      bar: 'def'
    }
  },
  created: function () {
    console.log(this.$data)
    // => { message: "goodbye", foo: "abc", bar: "def" }
  }
});
```

Hook functions with the same name are merged into an array so that all of them will be called. Mixin hooks will be called before the component’s own hooks.

```sh
var mixin = {
  created: function () {
    console.log('mixin hook called')
  }
}

new Vue({
  mixins: [mixin],
  created: function () {
    console.log('component hook called')
  }
})

// => "mixin hook called"
// => "component hook called"
```

Options that expect object values, for example `methods`, `components` and `directives`, will be merged into the same object. The component’s options will take priority when there are conflicting keys in these objects:

```sh
var mixin = {
  methods: {
    foo: function () {
      console.log('foo')
    },
    conflicting: function () {
      console.log('from mixin')
    }
  }
}

var vm = new Vue({
  mixins: [mixin],
  methods: {
    bar: function () {
      console.log('bar')
    },
    conflicting: function () {
      console.log('from self')
    }
  }
})

vm.foo() // => "foo"
vm.bar() // => "bar"
vm.conflicting() // => "from self"
```

Note that the same merge strategies are used in `Vue.extend()`.

## Important things to note
In the hierarchy of things in a Vue application, inside a component mixins are applied first by default. The component is applied second, so that it can override the mixin in any case. So it is important to always remember that when there is a kind of conflict of authority, the Vue component will always have the final say and overriding powers.
