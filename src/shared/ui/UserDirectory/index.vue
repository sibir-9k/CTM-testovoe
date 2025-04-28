<template>
	<div class="position-relative">
		<input
			class="form-control"
			:placeholder="placeholder"
			:value="displayValue"
			readonly
			@click="isOpen = true" />

		<div v-if="isOpen" class="dropdown-menu show w-100 p-0">
			<table class="table table-hover mb-0">
				<tbody>
					<tr
						v-for="item in items"
						:key="item.id ?? item[displayKey]"
						@click="select(item)"
						style="cursor: pointer">
						<td>{{ item[displayKey] }}</td>
					</tr>
				</tbody>
			</table>
			<button class="btn-close position-absolute top-0 end-0 m-2" @click.stop="isOpen = false" />
		</div>

		<div
			v-if="isOpen"
			class="position-fixed top-0 start-0 w-100 h-100"
			@click.self="isOpen = false"
			style="background: transparent; z-index: 10" />
	</div>
</template>

<script lang="ts" setup>
import { ref, computed, defineProps, defineEmits } from 'vue';


const props = defineProps({
	modelValue: { type: Object as () => Record<string, any> | null, default: null },
	items: { type: Array as () => Record<string, any>[], required: true },
	displayKey: { type: String, required: true },
	placeholder: { type: String, default: '' },
});

const emit = defineEmits(['update:modelValue']);
const isOpen = ref(false);

const displayValue = computed(() => {
	if (!props.modelValue) return '';
	return String(props.modelValue[props.displayKey]);
});

function select(item: Record<string, any>) {
	emit('update:modelValue', item);
	isOpen.value = false;
}
</script>

<style scoped>
.dropdown-menu {
	z-index: 20;
}
</style>
