<template>
  <div class="hello">
      <button @click="foo(2)">Button 2</button>
  </div>
</template>

<script>
import mixin from '../mixins/mixin1';
export default {
  name: 'Test2',
  mixins: [mixin],
}
</script>
