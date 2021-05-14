---
theme: ./theme
highlighter: shiki
---

<div class="mb-12">

# Advanced Vue Concepts

<p class="font-semibold">Shivam Mishra, Front End <a href="https://deepsource.io">DeepSourceHQ</a></p>

</div>

---

<h1 class="text-center">DeepSource</h1>

<img alt="deepsource" src="/images/deepsource.png">

---

<h1 class="text-center">Frappe Charts</h1>

<img alt="deepsource" src="/images/frappe-charts.png">

---

<h1 class="text-8xl font-black text-center mt-24">Let's Talk <span class="text-green-500">Vue</span></h1>

---

<div class="max-w-2xl mx-auto text-center">

# Vue Abstraction Heirarchy

<div class="mt-12">
  <v-clicks>
    <div class="w-82 h-18 flex items-center justify-center p-2 mx-auto mt-4 text-sm font-bold text-center transition-all transition border border-gray-200 rounded-md shadow-md  hover:text-gray-800 hover:shadow-lg hover:border-gray-300 duration-400">Components</div>
    <div class="w-82 h-18 flex items-center justify-center p-2 mx-auto mt-4 text-sm font-bold text-center transition-all transition border border-gray-200 rounded-md shadow-md  hover:text-gray-800 hover:shadow-lg hover:border-gray-300 duration-400">Mixins</div>
    <div class="w-82 h-18 flex items-center justify-center p-2 mx-auto mt-4 text-sm font-bold text-center transition-all transition border border-gray-200 rounded-md shadow-md  hover:text-gray-800 hover:shadow-lg hover:border-gray-300 duration-400">Directives</div>
  </v-clicks>
</div>

</div>

---

<h1 class="text-8xl font-black text-center mt-24">Components</h1>

---

# Components

<v-clicks>

- **Primary form of code reuse** offered by Vue
- A **component is a Vue instances** and they accept mostly the same options as `new Vue`
- An app is basically a **tree of nested components**
- Components accept **props**, manage their **state** and **emit** events

</v-clicks>

---

## Basic Structure of a components

```vue {1-3|5-15|17-19|7|8|9-11|12|13}
<template>
  <!-- HTML Template -->
</template>

<script>
export default {
  name: 'ComponentName',
  props: [ ... ],
  data() {
    return { ... }
  },
  methods: { ... },
  computed: { ... }
}
</script>

<style>
/* Styles */
</style>
```

---

## A Button Component

```vue {1-5|7-15|17-22|all}
<template>
  <button @click="onClick" class="button">
    <slot>Button</slot>
  </button>
</template>

<script>
export default {
  methods: {
    onClick() {
      this.$emit("click");
    },
  },
};
</script>

<style>
.button {
  padding: 6px 8px;
  background-color: #252525;
}
</style>
```

---

# Renderless Components

<v-clicks>

- A renderless component **doesn't render any of its own HTML**.
- **Only manages state and behavior**, exposing a **single scoped slot** that gives the parent/consumer complete control over what should actually be rendered.
- Renders exactly what you pass into it, without any extra elements

</v-clicks>

<!-- You might have been in a situation where you install a third-party UI component only to discover that because of one small tweak you need to make, you have to throw out the whole package?

Custom controls like dropdowns, date pickers, or autocomplete fields can be very complex to build with a lot of unexpected edge cases to deal with. Especially for strongly opinionated design systems

A renderless component is a component that doesn't render any of its own HTML.

Instead it only manages state and behavior, exposing a single scoped slot that gives the parent/consumer complete control over what should actually be rendered.

A renderless component renders exactly what you pass into it, without any extra elements: -->

---

<h1 class="text-center">Headless UI</h1>

<img alt="headless" src="/images/headless.png">

---

# Mixins

Mixins are a **flexible way to distribute reusable functionalities** for Vue components.

A mixin object **can contain any component options**. When a component uses a mixin, **all options in the mixin will be “mixed” into the component’s own options**.

<!--
It’s a common situation: you have two components that are pretty similar, they share the same basic functionality, but there’s enough that’s different about each of them that you come to a crossroads: do I split this component into two different components? Or do I keep one component, but create enough variance with props that I can alter each one?

Neither of these solutions is perfect: if you split it into two components, you run the risk of having to update it in two places if the functionality ever changes, defeating DRY premises. On the other hand, too many props can get really messy very quickly, and force the maintainer, even if it’s yourself, to understand a lot of context in order to use it, which can slow you down.
-->

---

## Modal Component

```vue {all|12|6,20-22|2,3,14,18|13-19,23}
<template>
  <button @click="toggleShow">Click to Toggle Modal</button>
  <div v-if="isShowing" class="modal">
    <h4>{{ title }}</h4>
    <slot></slot>
    <button @click="triggerAction">{{ actionLabel }}</button>
  </div>
</template>

<script>
export default {
  props: ['title', 'actionLabel']
  data() {
    return { isShowing: false }
  },
  methods: {
    toggleShow() {
      this.isShowing = !this.isShowing;
    },
    triggerAction() {
      this.$emit('success')
    }
  }
}
</script>
```

---

## Modal Component

```vue {all|12|6,20-22|2,3,14,18|13-19,23}
<template>
  <button @click="toggleShow">Click to Toggle Modal</button>
  <div v-if="isShowing" class="modal">
    <h4>{{ title }}</h4>
    <slot></slot>
    <button @click="triggerAction">{{ actionLabel }}</button>
  </div>
</template>

<script>
export default {
  props: ['title', 'actionLabel']
  data() {
    return { isShowing: false }
  },
  methods: {
    toggleShow() {
      this.isShowing = !this.isShowing;
    },
    triggerAction() {
      this.$emit('success')
    }
  }
}
</script>
```

---

## Tooltip Component

```vue {all|11-18}
<template>
  <button @mouseover="toggleShow">Hover to Toggle Tooltip</button>
  <div v-if="isShowing" class="tooltip">
    {{ text }}
  </div>
</template>

<script>
export default {
  props: ['text']
  data() {
    return { isShowing: false }
  },
  methods: {
    toggleShow() {
      this.isShowing = !this.isShowing;
    }
  }
}
</script>
```

---

## A Mixin to Toggle

```js {all|2|7|3-5|8-10|all}
const toggle = {
  data() {
    return {
      isShowing: false,
    };
  },
  methods: {
    toggleShow() {
      this.isShowing = !this.isShowing;
    },
  },
};
```

---

## Refactored Modal and Tooltip

```js
import { toggle } from './mixins/toggle'

export default {
  props: ['title', 'actionLabel']
  mixins: [toggle],
  methods: {
    triggerAction() {
      this.$emit('success')
    }
  }
}
```

```js
import { toggle } from './mixins/toggle'

export default {
  props: ['text']
  mixins: [toggle]
}
```

---

## A Mixin for Data Fetching

<v-clicks>

- Should find and **run the `fetch` method on creation**

- Check is fetch is **running**, **successful** or **errored**

</v-clicks>

<v-clicks>

```js
$fetch: {
  isLoading: () => { ... },
  isSuccess: () => { ... },
  isError: () => { ... },
  loading: false,
  error: null,
},
```

```js
this.$fetch.loading = true;
try {
  /* Run Fetch Code */
} catch (err) {
  this.$fetch.error = err;
} finally {
  this.$fetch.loading = false;
}
```

</v-clicks>

---

```js {all|2,14|4,8-10|5|6|7|4-10|15|18|20|all}
export default {
  data: function () {
    return {
      $fetch: {
        isLoading: () => this.$data.$fetch.loading,
        isSuccess: () => !this.$data.$fetch.loading && !this.$data.$fetch.error,
        isError: () => this.$data.$fetch.error !== null,
        loading: false,
        error: null,
      },
    };
  },

  created: async function () {
    if (this.$options && typeof this.$options.fetch === "function";) {
      this.$fetch.loading = true;
      try {
        await this.$options.fetch.call(this);
      } catch (err) {
        this.$fetch.error = err;
      } finally {
        this.$fetch.loading = false;
      }
    }
  },
};
```

---

## Take Away for Mixins

<div class="max-w-2xl">

A mixin allows you to encapsulate one piece of functionality so that you can use it in different components throughout the application.

- **Should be pure**: Should not modify or change things outside of the function’s scope
- **Merging Startegy**: When a mixin and the component itself contain overlapping options, they will be “merged” using appropriate strategies.
- **Not the only option**: Mixins are certainly not the only option available to you; higher order components, for example, allow you to compose similar functionality.

</div>

---

<h1 class="text-8xl font-black text-center mt-24">Directives</h1>

---

# Directives

<v-clicks>

Directives allow **low-level DOM access** on plain elements.

```html
<button v-tooltip="'You have 2 new messages.'"></button>
```

Custom directives allow you to create reusable pieces of low-level dom functions.

</v-clicks>

---

## Writing Custom Directives

Vue provides us with a comprehensive suite of hooks that are triggered at specific stages of rendering the element. The hooks are as follows:

<v-clicks>

- **`bind`** – This occurs once the directive is attached to the element.
- **`inserted`** – This hook occurs once the element is inserted into the parent DOM.
- **`update`** – This hook is called when the element updates, but children haven’t been updated yet.
- **`componentUpdated`** – This hook is called once the component _and_ the children have been updated.
- **`unbind`** – This hook is called once the directive is removed.

</v-clicks>

<v-click :at="6">

Vue documentation has a good example a `v-focus` directive with `autofocus` like behaviour for input components. You can check it out [here](https://vuejs.org/v2/guide/custom-directive.html#Intro).

</v-click>

---

## Outside Click Directive

```vue {all|3}
<template>
  <button v-on:click="toggle" class="dropdown-button">Menu</button>
  <div v-if="isOpen" v-outside-click="close" class="dropdown-body">
    <!-- Dropdown Body -->
  </div>
</template>

<script>
export default {
  name: 'ToyDropdown'
  data: {
	return {isOpen: false}
  },
  methods: {
	toggle() {
	  this.isOpen = !this.isOpen
	},
	close() {
	  this.isOpen = false
	}
  }
}
</script>
```

---

### Detecting clicks outside an element

<!-- Here we want a function close to be triggered when clicked outside the element we’ve created the binding with Let’s start with a function that does exactly that. -->

```js {all|3,5|4}
function onDocumentClick(e, el, fn) {
  let target = e.target;
  if (el !== target && !el.contains(target)) {
    fn(e);
  }
}
```

---

### Building the Directive

<v-clicks>

```js {all|3|4|5-7|9|all}
// Bind Event
export default {
  bind(el, binding) {
    const fn = binding.value;
    const click = function (e) {
      onDocumentClick(e, el, fn);
    };

    document.addEventListener("click", click);
  },
};
```

```js {3|4|5|all}
// Unbind Event
unbind(el) {
	const index = el.dataset.outsideClickIndex;
	const handler = // get handler
	document.removeEventListener('click', handler);
}
```

</v-clicks>

<!-- The bind, like other hooks receive a few arguments. The one we are interested is `binding` an object that contains the name of the directive, the value that is passed to it and more. -->

<!-- In our case, the value will be a function that will trigger on outside click. -->

<!-- This alone would work fine, however we need to remove the event listener on `unbind` this means we need to store the added event listener in the memory for reference later. This is simple to solve, all we need is an array, that we will store all the event listeners in. We will also attach an index to the data attributes of the element to recognise the index of the event listener. -->

<!-- Another enhancement we can do is to also add events for `touchstart` -->

<!-- With this our directive looks something like this -->

---

```js {1|3-5|8-18|19-24|9|11-16|17|20,21|22|23}
let instances = [];

function onDocumentClick(e, el, fn) {
  // document click function
}

export default {
  bind(el, binding) {
    el.dataset.outsideClickIndex = instances.length;

    const fn = binding.value;
    const click = function (e) {
      onDocumentClick(e, el, fn);
    };

    document.addEventListener("click", click);
    instances.push(click);
  },
  unbind(el) {
    const index = el.dataset.outsideClickIndex;
    const handler = instances[index];
    document.removeEventListener("click", handler);
    instances.splice(index, 1);
  },
};
```

---

### Using the Directive

```js
import outsideClickDirective from "../../directives/outside-click";

Vue.directive("outside-click", outsideClickDirective);
```

---

<div class="text-center">
<h1 class="text-5xl font-black text-center mt-24">That's all Folks</h1>
<p class="text-center mx-auto">hey[at]shivam.dev</p>
</div>

---

<div class="text-center">
<h1 class="text-5xl font-black text-center mt-24">My Team is Hiring</h1>
<p class="text-center mx-auto">

[careers.deepsource.io](https://careers.deepsource.io)

</p>
</div>

---

# Links

- [Vue Docs: Components](https://vuejs.org/v2/guide/components.html)
- [Vue Docs: Mixins](https://vuejs.org/v2/guide/mixins.html)
- [Vue Docs: Directives](https://vuejs.org/v2/guide/custom-directive.html)
- [Outside Click Directive](https://shivam.dev/blog/outside-click)
- [Renderless Components by Adam Wathan](https://adamwathan.me/renderless-components-in-vuejs/)
