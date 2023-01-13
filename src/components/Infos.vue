<template>
  <div>
    <div class="infos">
      <div class="a">Not ChatGPT</div>
      <div>Yeah, its the same thing as chat gpt but made by me</div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'Infos',
  components: {},
  data() {
    return {};
  },
});
</script>

<style lang="scss" scoped>
@import url('https://fonts.googleapis.com/css2?family=Pacifico&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Ropa+Sans&display=swap');

.infos {
  color: white;
}

.text {
  position: absolute;
  font-family: 'Ropa Sans', sans-serif;
  font-size: 6.2em;
  font-weight: bold;
  text-shadow: 0px 0px 1px rgb(167, 167, 167), 0px 1px 1px rgb(167, 167, 167),
    0px 2px 1px rgb(167, 167, 167);
}

@keyframes cycle {
  0% {
    text-shadow: 0px 0px 100px rgba(11, 124, 199, 0.5);
  }
  20% {
    text-shadow: 0px 0px 100px rgba(168, 11, 199, 0.5);
  }
  40% {
    text-shadow: 0px 0px 100px rgba(11, 199, 96, 0.5);
  }
  60% {
    text-shadow: 0px 0px 100px rgba(199, 11, 11, 0.5);
  }
  90% {
    text-shadow: 0px 0px 100px rgba(199, 96, 11, 0.5);
  }
}

.text::after {
  animation: cycle 10s linear infinite;
}
</style>
