<template>
<div>
	<portal to="icon"><fa :icon="faHashtag"/></portal>
	<portal to="title">{{ $route.params.tag }}</portal>

	<x-notes ref="notes" :pagination="pagination" @before="before" @after="after"/>
</div>
</template>

<script lang="ts">
import Vue from 'vue';
import { faHashtag } from '@fortawesome/free-solid-svg-icons';
import Progress from '../scripts/loading';
import XNotes from '../components/notes.vue';

export default Vue.extend({
	metaInfo() {
		return {
			title: '#' + this.$route.params.tag
		};
	},

	components: {
		XNotes
	},

	data() {
		return {
			pagination: {
				endpoint: 'notes/search-by-tag',
				limit: 10,
				params: () => ({
					tag: this.$route.params.tag,
				})
			},
			faHashtag
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
