<!-- eslint-disable vue/no-mutating-props -->
<template>
	<div>
		<div>
			<div class="q-pa-md">
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
								<q-tooltip
									v-if="maximizedToggle"
									class="bg-white text-primary"
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
								<q-tooltip
									v-if="!maximizedToggle"
									class="bg-white text-primary"
									>Maximize</q-tooltip
								>
							</q-btn>
							<q-btn dense flat icon="close" to="/">
								<q-tooltip class="bg-white text-primary"
									>Close</q-tooltip
								>
							</q-btn>
						</q-bar>
						<q-card-section class="row items-center">
							<Display
								:messages="messages"
								class="display"
							></Display>
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
		props: ['openModal'],
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
				dialog: ref(true),
				dialogFlag: ref(false),
				maximizedToggle: ref(false),
				input: ref(false),
			};
		},
		components: { Display },
		methods: {
			handleDialog() {
				!this.dialogFlag;
			},
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
					this.messages.push({
						name: 'bot',
						message: msg,
						textcolor: 'white',
						bgcolor: 'purple',
					});
				} catch (err) {
					console.log(err);
				}
			},

			async sendChat() {
				try {
					this.input = true;
					const { data } = await this.$axios.post(
						'https://chat-ai-backend.vercel.app',
						{
							question: this.text,
						}
					);
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
	});
</script>
<style lang="scss" scoped>
	.chatInput {
		width: 100%;
	}

	@media screen and (max-width: 850px) {
		.button {
			width: 150px;
			height: 50px;
			border-radius: 8px;
			background-color: black;
			border: none;
			color: white;

			margin-top: 15px;
			font-size: 1.2em;
		}
	}
	@media screen and (min-width: 851px) {
		.button {
			width: 150px;
			height: 50px;
			border-radius: 8px;
			background-color: black;
			border: none;
			color: white;

			margin-top: 15px;
			font-size: 1.2em;
		}
	}
</style>
