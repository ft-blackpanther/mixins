<template>
  <div class="hello">
      <button @click="foo(1)">Button 1</button>
  </div>
</template>

<script>
import mixin from '../mixins/mixin1';
export default {
  name: 'Test1',
  mixins: [mixin],
}
</script>
