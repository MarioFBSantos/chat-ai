<template>
  <!-- <img src="images/landing.jpg" class="image" loading="lazy" draggable="false" /> -->
  <div class="layout q-pa-lg">
    <div><Info class="info" /></div>
    <div class="q-py-lg">
      <Chat class="chat" />
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import Chat from '../components/Chat.vue';
import Info from '../components/Infos.vue';

export default defineComponent({
  name: 'PageIndex',
  components: { Chat, Info },
  setup() {
    return {};
  },
});
</script>

<style lang="scss" scoped>
img {
  max-width: 100%;
  display: block;
  height: auto;
  user-select: none;
}

@media screen and (max-width: 800px) {
  .layout {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-content: stretch;
    flex-wrap: nowrap;
    align-items: center;
  }
}
</style>
