<script setup>
import { ref } from "vue"

const header = ref("Shopping List App")
const editing = ref(false)
const items = ref([
	{ id: 1, label: "10 party hats", purchased: true, highPriority: false },
	{ id: 2, label: "20 balloons", purchased: true, highPriority: false },
	{ id: 3, label: "5 candles", purchased: false, highPriority: true },
])
const newItem = ref("")
const newItemHighPriority = ref(false)
const saveItem = () => {
	items.value.push({
		id: items.value.length + 1,
		label: newItem.value,
		highPriority: newItemHighPriority.value,
	})
	newItem.value = ""
	newItemHighPriority.value = false
}
const doEdit = (e) => {
	editing.value = e
	newItem.value = ""
}

const togglePurchsed = (item) => {
	item.purchased = !item.purchased
}
</script>

<template>
	<div>
		<h1 class="text-4xl mb-4 font-bold inline mr-5">{{ header }}</h1>
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
			class="px-2 py-1 mt-2 mr-2"
			v-model.trim="newItem"
			type="text"
			placeholder="Add an item"
		/>
		<label>
			<input class="mr-1" type="checkbox" v-model="newItemHighPriority" />
			<span>High Priority</span>
		</label>
		<br />
		<!--  button is disabled if newItem is empty -->
		<button
			:disabled="newItem.length === 0"
			:class="[
				newItem.length === 0
					? 'bg-gray-400 px-3 py-2 rounded-lg text-white font-bold text-lg mt-3'
					: 'bg-blue-400 px-3 py-2 rounded-lg text-white font-bold text-lg mt-3',
			]"
		>
			Save Item
		</button>
	</form>
	<ul class="mt-2">
		<li
			@click="togglePurchsed(item)"
			v-for="item in items"
			:class="{
				'line-through': item.purchased,
				'text-blue-500 font-bold': item.highPriority,
			}"
			:key="item.id"
		>
			{{ item.label }}
		</li>
		<p v-if="!items.length">Nothing to see here</p>
	</ul>
</template>
