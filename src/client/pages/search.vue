<template>
<div>
	<portal to="icon"><fa :icon="faSearch"/></portal>
	<portal to="title">{{ $t('searchWith', { q: $route.query.q }) }}</portal>
	<x-notes ref="notes" :pagination="pagination" @before="before" @after="after"/>
</div>
</template>

<script lang="ts">
import Vue from 'vue';
import { faSearch } from '@fortawesome/free-solid-svg-icons';
import Progress from '../scripts/loading';
import XNotes from '../components/notes.vue';

export default Vue.extend({
	metaInfo() {
		return {
			title: this.$t('searchWith', { q: this.$route.query.q }) as string
		};
	},

	components: {
		XNotes
	},

	data() {
		return {
			pagination: {
				endpoint: 'notes/search',
				limit: 10,
				params: () => ({
					query: this.$route.query.q,
				})
			},
			faSearch
		};
	},

	watch: {
		$route() {
			(this.$refs.notes as any).reload();
		}
	},

	methods: {
		before() {
			Progress.start();
		},

		after() {
			Progress.done();
		}
	}
});
</script>
