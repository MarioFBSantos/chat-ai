<template>
  <div class="layout q-mx-lg">
    <Chat class="chat"></Chat>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';
import Chat from '../components/Chat.vue';

export default defineComponent({
  name: 'PageIndex',
  components: {
    Chat,
  },
  setup() {
    const openModal = ref(false);
    return {
      openModal,
    };
  },
});
</script>

<style lang="scss" scoped></style>
