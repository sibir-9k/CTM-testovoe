<template>
	<div class="container mt-4">
		<h3>1. Статус поставки</h3>
		<UserDirectory
			v-model="selectedStatus"
			:items="statusOptions"
			displayKey="description"
			placeholder="Выберите статус" />
		<p>Выбран статус: {{ selectedStatus }}</p>

		<h3 class="mt-4">2. Режим перемещения</h3>
		<UserDirectory
			v-model="selectedMode"
			:items="modeOptions"
			displayKey="description"
			placeholder="Выберите режим" />
		<p>Выбран режим: {{ selectedMode }}</p>
	</div>
</template>

<script lang="ts" setup>
import { ref } from 'vue';
import UserDirectory from '../shared/ui/UserDirectory/index.vue';

interface Option {
	id: number;
	description: string;
}

const selectedStatus = ref<Option | null>(null);
const selectedMode = ref<Option | null>(null);

const statusOptions: Option[] = [
	{ id: 0, description: 'Формируется' },
	{ id: 1, description: 'Товар прибыл' },
	{ id: 2, description: 'Срочная поставка' },
	{ id: 3, description: 'Оформление ДТ' },
	{ id: 4, description: 'ДТ выпущена' },
	{ id: 5, description: 'Поставка закрыта' },
];

const modeOptions: Option[] = [
	{ id: 1, description: 'Импорт' },
	{ id: 2, description: 'Экспорт' },
];
</script>
