<template>
<div class="">
	<portal to="icon"><fa :icon="faShareAlt"/></portal>
	<portal to="title">{{ $t('share') }}</portal>

	<section class="_card">
		<div class="_title" v-if="title">{{ title }}</div>
		<div class="_content">
			<div>{{ text }}</div>
			<mk-button @click="post()" v-if="!posted">{{ $t('post') }}</mk-button>
			<mk-button primary @click="close()" v-else>{{ $t('close') }}</mk-button>
		</div>
		<div class="_footer" v-if="url">{{ url }}</div>
	</section>
</div>
</template>

<script lang="ts">
import Vue from 'vue';
import { faShareAlt } from '@fortawesome/free-solid-svg-icons';
import i18n from '../i18n';
import PostFormDialog from '../components/post-form-dialog.vue';
import MkButton from '../components/ui/button.vue';

export default Vue.extend({
	i18n,

	metaInfo() {
		return {
			title: this.$t('share') as string
		};
	},

	components: {
		MkButton
	},

	data() {
		return {
			title: null,
			text: null,
			url: null,
			posted: false,

			faShareAlt
		}
	},

	created() {
		const urlParams = new URLSearchParams(window.location.search);
		this.title = urlParams.get('title');
		this.text = urlParams.get('text');
		this.url = urlParams.get('url');
	},

	mounted() {
		this.post();
	},

	methods: {
		post() {
			let text = '';
			if (this.title) text += `【${this.title}】\n`;
			if (this.text) text += `${this.text}\n`;
			if (this.url) text += `${this.url}`;
			this.$root.new(PostFormDialog, {
				instant: true,
				initialText: text.trim()
			}).$once('posted', () => {
				this.posted = true;
				this.$root.dialog({
					type: 'success',
					iconOnly: true, autoClose: true
				});
			});
		},
		close() {
			window.close()
		}
	}
});
</script>

<style lang="scss" scoped>
</style>
