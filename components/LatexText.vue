<template>
	<text>
		<text v-for="(seg, index) in segments" :key="index" :class="{ 'latex-math': isMath(seg) }">
			{{ cleanMath(seg) }}
		</text>
	</text>
</template>

<script setup>
import { computed } from 'vue';
const props = defineProps({ text: [String, Number] });

const segments = computed(() => {
	if (!props.text) return [];
	return String(props.text).split(/(\$[^\$]+\$)/g);
});

const isMath = (str) => str && str.startsWith('$') && str.endsWith('$');
const cleanMath = (str) => isMath(str) ? str.slice(1, -1) : str;
</script>

<style scoped>
.latex-math { color: #2563eb; font-style: italic; margin: 0 4px; font-family: serif; }
</style>