<script>
import Vue from 'vue';
import ButtonToDropdown from '@/button-to-dropdown.vue';

export default Vue.extend({
  name: 'ServeDev',
  components: {
    ButtonToDropdown
  }
});
</script>

<template>
  <div id="app">
    <button-to-dropdown />
  </div>
</template>
