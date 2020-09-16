# @vue/lit 🖖🔥

Proof of concept mini custom elements framework powered by [@vue/reactivity](https://github.com/vuejs/vue-next/tree/master/packages/reactivity) and [lit-html](https://lit-html.polymer-project.org/). The "framework" itself is just ~60 lines of code and the two libraries weigh in at ~6kb min + brotli combined.

The API is almost identical to [Vue Composition API](https://composition-api.vuejs.org), but defines native custom elements underneath.

## Example

```js
import {
  defineComponent,
  reactive,
  html,
  onMounted,
  onUpdated,
  onUnmounted
} from 'https://unpkg.com/@vue/lit'

defineComponent('my-component', (props) => {
  const state = reactive({ show: true })
  const toggle = () => {
    state.show = !state.show
  }

  return () => html`
    <button @click=${toggle}>toggle child</button>
    ${state.show ? html`<my-child></my-child>` : ``}
  `
})

defineComponent('my-child', (props) => {
  const state = reactive({ count: 0 })
  const increase = () => {
    state.count++
  }

  onMounted(() => {
    console.log('child mounted')
  })

  onUpdated(() => {
    console.log('child updated')
  })

  onUnmounted(() => {
    console.log('child unmounted')
  })

  return () => html`
    <p>${props.msg}</p>
    <p>${state.count}</p>
    <button @click=${increase}>increase</button>
  `
})
```
