<template>
	<div class="container mt-4">
		<h3>1. Статус поставки</h3>
		<UserDirectory
			v-model:modelValue="selectedStatus"
			:items="statusOptions"
			displayKey="description"
			placeholder="Выберите статус" />

		<h3 class="mt-4">2. Режим перемещения</h3>
		<UserDirectory
			v-model:modelValue="selectedMode"
			:items="modeOptions"
			displayKey="description"
			placeholder="Выберите режим" />

		<pre class="mt-3">Выбран статус: {{ selectedStatus }}</pre>
		<pre>Выбран режим: {{ selectedMode }}</pre>
	</div>
</template>

<script lang="ts" setup>
import { ref } from 'vue';
import UserDirectory from '../shared/ui/UserDirectory/index.vue';
import type { StatusOption, ModeOption } from '../entities/delivery';

const statusOptions = ref<StatusOption[]>([
	{
		code: 0,
		description: 'Формируется',
	},
	{
		code: 10,
		description: 'Товар прибыл',
	},
	{
		code: 20,
		description: 'Товар прибыл (срочная поставка)',
	},
	{
		code: 30,
		description: 'Оформление ДТ',
	},
	{
		code: 40,
		description: 'ДТ выпущена',
	},
	{
		code: 50,
		description: 'Поставка закрыта',
	},
]);

const modeOptions = ref<ModeOption[]>([
	{ id: 1, description: 'Импорт' },
	{ id: 2, description: 'Экспорт' },
]);

const selectedStatus = ref<StatusOption | null>(null);
const selectedMode = ref<ModeOption | null>(null);
</script>
