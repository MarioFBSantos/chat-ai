<template>
  <div>
    <div>
      <div class="q-pa-md">
        <q-btn label="Open Dialog" color="primary" @click="dialog = true" />

        <q-dialog
          v-model="dialog"
          persistent
          transition-show="flip-down"
          transition-hide="flip-up"
          :maximized="maximizedToggle"
        >
          <q-card>
            <q-bar>
              <q-space />

              <q-btn
                dense
                flat
                icon="minimize"
                @click="maximizedToggle = false"
                :disable="!maximizedToggle"
              >
                <q-tooltip v-if="maximizedToggle" class="bg-white text-primary"
                  >Minimize</q-tooltip
                >
              </q-btn>
              <q-btn
                dense
                flat
                icon="crop_square"
                @click="maximizedToggle = true"
                :disable="maximizedToggle"
              >
                <q-tooltip v-if="!maximizedToggle" class="bg-white text-primary"
                  >Maximize</q-tooltip
                >
              </q-btn>
              <q-btn dense flat icon="close" v-close-popup>
                <q-tooltip class="bg-white text-primary">Close</q-tooltip>
              </q-btn>
            </q-bar>
            <q-card-section class="row items-center">
              <Display :messages="messages" class="display"></Display>
            </q-card-section>

            <q-card-section class="row items-center">
              <q-input
                outlined
                v-model="text"
                label="Type here"
                @keydown.enter="insertUserMsg(text)"
                class="chatInput q-mt-xs"
                :disable="input"
              />
            </q-card-section>

            <!-- Notice v-close-popup -->
          </q-card>
        </q-dialog>
      </div>
    </div>
  </div>
</template>
<script lang="ts">
import { defineComponent, ref, reactive } from 'vue';
import iMessage from './iMessage';
import Display from '../components/display.vue';

export default defineComponent({
  name: 'chat',
  setup() {
    const messages = ref<iMessage[]>([
      {
        name: 'you',
        message: 'Ask something',
        textcolor: 'white',
        bgcolor: 'primary',
      },
    ]);
    return {
      text: ref(''),
      messages,
      dialog: ref(false),
      maximizedToggle: ref(false),
      input: ref(false),
    };
  },
  components: { Display },
  updated() {
    // this.scrollToEnd();
  },
  methods: {
    async insertUserMsg(msg: string) {
      const obj = reactive({
        name: 'you',
        message: msg,
        textcolor: 'white',
        bgcolor: 'primary',
      });

      this.messages.push(obj);
      await this.sendChat();
      this.text = '';
    },

    insertBotMsg(msg: string) {
      try {
        console.log(msg);
        this.messages.push({
          name: 'bot',
          message: msg,
          textcolor: 'gray',
          bgcolor: 'active',
        });
      } catch (err) {
        console.log(err);
      }
    },

    // scrollToEnd() {
    //   const content = this.$refs.container;
    //   // eslint-disable-next-line @typescript-eslint/ban-ts-comment
    //   // @ts-ignore
    //   content.scrollTop = content.scrollHeight;
    // },

    async sendChat() {
      try {
        this.input = true;
        const { data } = await this.$axios.post('http://localhost:8000', {
          question: this.text,
        });
        this.text = '';
        // eslint-disable-next-line @typescript-eslint/no-unsafe-argument, @typescript-eslint/no-unsafe-member-access
        this.insertBotMsg(data.bot);
        this.input = false;
      } catch (err) {
        console.log(err);
        this.input = false;
      }
    },
  },
  mounted() {
    // this.scrollToEnd();
  },
});
</script>
<style lang="scss" scoped></style>
