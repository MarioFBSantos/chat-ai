<template>
  <div class="display q-pa-lg" ref="display">
    <q-chat-message
      v-for="(message, index) in messages"
      :key="index"
      :name="message.name"
      :sent="message.name === 'you' ? true : false"
      :text-color="message.textcolor"
      :bg-color="message.bgcolor"
      class="message"
    >
      <div>
        {{ message.message || 'Digite a primeira mensagem' }}
      </div>
    </q-chat-message>
  </div>
</template>
<script lang="ts">
import { defineComponent, ref, PropType } from 'vue';

export interface Messages {
  name: string;
  message: string;
  textcolor: string;
  bgcolor: string;
}
export default defineComponent({
  name: 'display',
  setup() {
    return {
      text: ref(''),
      dialog: ref(false),
      maximizedToggle: ref(true),
    };
  },
  props: {
    messages: Array as PropType<Messages[]>,
  },
  updated() {
    this.scrollToEnd();
  },
  methods: {
    scrollToEnd() {
      const content = this.$refs.display;
      // eslint-disable-next-line @typescript-eslint/ban-ts-comment
      // @ts-ignore
      content.scrollTop = content.scrollHeight;
    },
  },
  mounted() {
    this.scrollToEnd();
  },
});
</script>
<style lang="scss" scoped>
.display {
  width: 100vw;
  height: 70vh;
  overflow-y: scroll;
}
.chatbox {
  color: white;
}

.chatInput {
  background-color: #fff;
  border-radius: 5px;
}
::-webkit-scrollbar {
  width: 10px;
}
::-webkit-scrollbar-track {
  background: #222222;
}

/* Handle */
::-webkit-scrollbar-thumb {
  background: #888;
  border-radius: 3px;
}

/* Handle on hover */
::-webkit-scrollbar-thumb:hover {
  background: #555;
}
</style>
