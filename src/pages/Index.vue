<template>
  <div class="layout q-mx-lg">
    <div><Info class="info q-mx-lg" /></div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';
import Info from '../components/Infos.vue';

export default defineComponent({
  name: 'PageIndex',
  components: { Info },
  setup() {
    const openModal = ref(false);
    return {
      openModal,
    };
  },
});
</script>

<style lang="scss" scoped>
.layout {
  height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: flex-end;
  justify-content: center;
}
img {
  max-width: 100%;
  display: block;
  height: auto;
  user-select: none;
}

@media screen and (max-width: 1400px) {
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
