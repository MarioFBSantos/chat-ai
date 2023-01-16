<template>
  <div>
    <div class="infos">
      <div class="title">Not ChatGPT</div>
      <div class="subTitle">
        Yeah, its the same thing as chat gpt but made by Mario Santos
      </div>
      <RouterLink to="/chat" class="button q-mt-lg glow-on-hover">OPEN CHAT</RouterLink>
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

.button {
  width: 150px;
  height: 50px;
  border-radius: 8px;
  background-color: black;
  border: none;
  color: white;
  font-size: 1.2em;
  text-align: center;
  text-decoration: none;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: transform 0.2s;
}
.button:hover {
  transform: scale(105%);
}
.infos {
  color: white;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.title {
  font-family: 'Ropa Sans', sans-serif;
  font-size: 9.2em;
  text-align: center;
  color: rgb(0, 0, 0);
  text-shadow: 2px 1px 0px #363636;
}
.title::after {
  mix-blend-mode: difference;
}
.subTitle {
  color: rgb(179, 179, 179);
  text-shadow: 1px 1px 0px #0f0f0f;
  font-size: 1.1em;
}

@media screen and (max-width: 1400px) {
  .title {
    color: rgb(0, 0, 0);
    text-shadow: 1px 1px 0px #ffffff;
  }
}

// button

.glow-on-hover {
  width: 220px;
  height: 50px;
  border: none;
  outline: none;
  color: #fff;
  background: #111;
  cursor: pointer;
  position: relative;
  z-index: 0;
  border-radius: 10px;
}

.glow-on-hover:before {
  content: '';
  background: linear-gradient(
    45deg,
    #ff0000,
    #ff7300,
    #fffb00,
    #48ff00,
    #00ffd5,
    #002bff,
    #7a00ff,
    #ff00c8,
    #ff0000
  );
  position: absolute;
  top: -2px;
  left: -2px;
  background-size: 400%;
  z-index: -1;
  filter: blur(5px);
  width: calc(100% + 4px);
  height: calc(100% + 4px);
  animation: glowing 20s linear infinite;
  opacity: 0;
  transition: opacity 0.3s ease-in-out;
  border-radius: 10px;
}

.glow-on-hover:active {
  color: #000;
}

.glow-on-hover:active:after {
  background: transparent;
}

.glow-on-hover:hover:before {
  opacity: 1;
}

.glow-on-hover:after {
  z-index: -1;
  content: '';
  position: absolute;
  width: 100%;
  height: 100%;
  background: #111;
  left: 0;
  top: 0;
  border-radius: 10px;
}

@keyframes glowing {
  0% {
    background-position: 0 0;
  }
  50% {
    background-position: 400% 0;
  }
  100% {
    background-position: 0 0;
  }
}
</style>
