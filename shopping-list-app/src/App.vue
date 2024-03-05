<script setup>
import { ref } from "vue"

const header = ref("Shopping List App")
const editing = ref(false)
const items = ref([
	// { id: 1, label: "10 party hats" },
	// { id: 2, label: "20 balloons" },
	// { id: 3, label: "5 candles" },
])
const newItem = ref("")
const newItemHighPriority = ref(false)
const saveItem = () => {
	items.value.push({ id: items.value.length + 1, label: newItem.value })
	newItem.value = ""
}
const doEdit = (e) => {
	editing.value = e
	newItem.value = ""
}
</script>

<template>
	<div>
		<h1 class="text-4xl mb-4 font-bold">{{ header }}</h1>
		<button
			v-if="editing"
			@click="doEdit(false)"
			class="bg-gray-400 px-3 py-2 rounded-lg text-white font-bold text-lg"
		>
			Cancel
		</button>

		<button
			v-else
			@click="doEdit(true)"
			class="bg-blue-400 px-3 py-2 rounded-lg text-white font-bold text-lg"
		>
			Add Item
		</button>
	</div>
	<form v-if="editing" @submit.prevent="saveItem">
		<input
			class="px-2 py-1 mr-2"
			v-model.trim="newItem"
			type="text"
			placeholder="Add an item"
		/>
		<label>
			<input class="m-1" type="checkbox" v-model="newItemHighPriority" />
			<span>High Priority</span>
		</label>
		<br />
		<!--  button is disabled if newItem is empty -->
		<button
			:disabled="newItem.length === 0"
			class="bg-blue-400 px-3 py-2 rounded-lg text-white font-bold text-lg mt-3"
		>
			Save Item
		</button>
	</form>
	<ul class="mt-2">
		<li class="leading-loose text-xl" v-for="{ id, label } in items" :key="id">
			{{ label }}
		</li>
		<p v-if="!items.length">Nothing to see here</p>
	</ul>
</template>
