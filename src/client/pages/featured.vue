<template>
<div>
	<portal to="icon"><fa :icon="faFireAlt"/></portal>
	<portal to="title">{{ $t('featured') }}</portal>
	<x-notes ref="notes" :pagination="pagination" @before="before" @after="after"/>
</div>
</template>

<script lang="ts">
import Vue from 'vue';
import { faFireAlt } from '@fortawesome/free-solid-svg-icons';
import Progress from '../scripts/loading';
import XNotes from '../components/notes.vue';

export default Vue.extend({
	metaInfo() {
		return {
			title: this.$t('featured') as string
		};
	},

	components: {
		XNotes
	},

	data() {
		return {
			pagination: {
				endpoint: 'notes/featured',
				limit: 10,
				offsetMode: true
			},
			faFireAlt
		};
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
