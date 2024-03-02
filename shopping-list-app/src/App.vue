<script setup>
import { ref } from "vue"

const header = ref("Shopping List App")
const items = ref([
	{ id: 1, label: "10 party hats" },
	{ id: 2, label: "20 balloons" },
	{ id: 3, label: "5 candles" },
])
const newItem = ref("")
const newItemHighPriority = ref(false)
const iceCreamFlavors = ref([])
</script>

<template>
	<h1 class="text-4xl mb-4 font-bold">{{ header }}</h1>
	<input
		class="px-2 py-1 mr-2"
		v-model.trim="newItem"
		type="text"
		placeholder="Add an item"
	/>
	<label>
		<input class="m-1" type="checkbox" v-model="newItemHighPriority" />
		<span>High Priority:</span>
	</label>
	<ul class="mt-2">
		<li class="leading-loose text-xl" v-for="{ id, label } in items" :key="id">
			{{ label }}
		</li>
		<li class="leading-loose text-xl">
			{{ newItem }}
		</li>
	</ul>
</template>
