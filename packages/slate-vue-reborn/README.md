# Slate-vue for vue2.x

## Install

in npm

```javascript
npm install slate-vue
```

in yarn

```javascript
yarn add slate-vue
```

## Usage

### quick start

import

```javascript
import Vue from 'vue'
import { SlatePlugin } from 'slate-vue-reborn';
Vue.use(SlatePlugin)
```

use

```vue
<template>
  <Slate :value="value">
    <Editable placeholder="Enter some plain text..."></Editable>
  </Slate>
</template>

<script>
  import {Slate, Editable} from 'slate-vue-reborn'

  // this value is for editor
  const initialValue = [
    {
      children: [
        { text: 'This is editable plain text, just like a <textarea>!' },
      ],
    },
  ]
  export default {
    name: 'index',
    components: {
      Slate,
      Editable
    },
    data() {
      return {
        value: JSON.stringify(initialValue)
      }
    }
  };
</script>
```

### more detail

Vue's [jsx](https://github.com/vuejs/jsx) and [tsx](https://github.com/wonderful-panda/vue-tsx-support) grammar is recommend, but SFC is also supported.

Most of the usage is same with [slate-react](https://github.com/ianstormtaylor/slate/tree/master/packages/slate-react). Here are same difference as guideline:

## Guideline

### get editor instance

```javascript
this.$editor
```

If you want to apply some plugins(e.g. slate-history), use editorCreated hook:

```javascript
Vue.use(SlatePlugin, {
  editorCreated(editor) {
    withHistory(editor)
  }
})
```

It will be called after each editor created.

### renderElement, renderLeaf

ReturnType must be any legal type which is equal with the first argument in Vue's createElement, please [see](https://vuejs.org/v2/guide/render-function.html#createElement-Arguments).

### select, focus , readonly

Use Vue.mixin
```javascript
import {SelectedMixin, FocusedMixin} from 'slate-vue-reborn'
```
And you will get selected, focused data in your component

Use global inject: ```inject: ['readOnly]``` 

And you will get readOnly data in your component

### useEffect, useRef

```javascript
import {useEffect, useRef} from 'slate-vue-reborn'
```

Same as react hooks. Forked from [vue-hooks](https://github.com/yyx990803/vue-hooks).

### fragment

```javascript
import {fragment} from 'slate-vue-reborn'
```

Forked from [vue-fragment](https://github.com/Thunberg087/vue-fragment)

### VueEditor

```javascript
import {VueEditor} from 'slate-vue-reborn'
```

Same api with [react-editor](https://docs.slatejs.org/libraries/slate-react#reacteditor)

## Problems

### Doesn't change?

If your component is related to the editor(like toolbar), you must add slateMixin for rerender:

```javascript
import {SlateMixin} from 'slate-vue-reborn'
```

### Nuxtjs

For Nuxtjs, you must add ``slate-vue`` and ``vue-tsx-support`` into your transpile option in nuxt.config.js

```javascript
build: { 
  transpile: ['slate-vue', 'vue-tsx-support'] 
}
```
