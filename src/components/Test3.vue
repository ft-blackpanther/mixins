<template>
  <div class="hello">
      <button @click="foo(2)">Button 2</button>
  </div>
</template>

<script>
import mixin from '../mixins/mixin2';
export default {
  name: 'Test3',
  mixins: [mixin],
  data: () => {
    return {
      message: 'goodbye',
      bar: 'def'
    }
  },
  created() {
    console.log(this.$data)
    // => { message: "goodbye", foo: "abc", bar: "def" }
  }
}
</script>
