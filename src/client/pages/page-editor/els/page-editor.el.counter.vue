<template>
<x-container @remove="() => $emit('remove')" :draggable="true">
	<template #header><fa :icon="faBolt"/> {{ $t('_pages.blocks.counter') }}</template>

	<section style="padding: 0 16px 0 16px;">
		<mk-input v-model="value.name"><template #prefix><fa :icon="faMagic"/></template><span>{{ $t('_pages.blocks._counter.name') }}</span></mk-input>
		<mk-input v-model="value.text"><span>{{ $t('_pages.blocks._counter.text') }}</span></mk-input>
		<mk-input v-model="value.inc" type="number"><span>{{ $t('_pages.blocks._counter.inc') }}</span></mk-input>
	</section>
</x-container>
</template>

<script lang="ts">
import Vue from 'vue';
import { faBolt, faMagic } from '@fortawesome/free-solid-svg-icons';
import i18n from '../../../i18n';
import XContainer from '../page-editor.container.vue';
import MkInput from '../../../components/ui/input.vue';

export default Vue.extend({
	i18n,

	components: {
		XContainer, MkInput
	},

	props: {
		value: {
			required: true
		},
	},

	data() {
		return {
			faBolt, faMagic
		};
	},

	created() {
		if (this.value.name == null) Vue.set(this.value, 'name', '');
	},
});
</script>
