<template>
	<div class="position-relative">
		<input
			type="text"
			class="form-control"
			:placeholder="placeholder"
			@focus="openList"
			@click="openList"
			:value="displayValue"
			readonly />
		<div v-if="isOpen" class="dropdown-menu show w-100 p-0">
			<table class="table table-hover mb-0">
				<tbody>
					<tr
						v-for="item in items"
						:key="getKey(item)"
						@click="select(item)"
						style="cursor: pointer">
						<td>{{ item[displayKey] }}</td>
					</tr>
				</tbody>
			</table>
			<button class="btn-close position-absolute top-0 end-0 m-2" @click="closeList"></button>
		</div>
		<div
			v-if="isOpen"
			class="position-fixed top-0 start-0 w-100 h-100"
			style="background: transparent; z-index: 10"
			@click="closeList" />
	</div>
</template>
<script lang="ts" setup>
import { ref, computed, defineProps, defineEmits } from 'vue';
interface Props<T> {
	items: T[];
	displayKey: keyof T;
	itemKey?: (item: T) => string | number;
	placeholder?: string;
}
const props = defineProps<Props<any>>();
const emit = defineEmits<{
	(e: 'update:modelValue', value: any): void;
}>();
const isOpen = ref(false);
const selected = ref<any | null>(null);
function openList() {
	isOpen.value = true;
}
function closeList() {
	isOpen.value = false;
}
const displayValue = computed(() =>
	selected.value ? String(selected.value[props.displayKey]) : ''
);
function getKey(item: any) {
	return props.itemKey ? props.itemKey(item) : displayValue.value;
}
function select(item: any) {
	selected.value = item;
	emit('update:modelValue', item);
	closeList();
}
</script>
<style scoped>
.dropdown-menu {
	z-index: 20;
}
</style>
