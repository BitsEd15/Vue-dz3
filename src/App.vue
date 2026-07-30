<script setup>
	import { ref } from 'vue';

	import ZadanineFirst from './components/ZadanineFirst.vue';
	import ZadanieSecond from './components/ZadanieSecond.vue';

	const zadacha1 = ref(true)
	const zadacha2 = ref(false)

	const toggleTask1 = ()=>{
		zadacha1.value=!zadacha1.value
		zadacha2.value = false 
	}

	const toggleTask2 = ()=>{
		zadacha2.value=!zadacha2.value
		zadacha1.value = false 
	}
</script>

<template>
	<div>
	<div>
		<button @click="toggleTask1">Задача 1</button>
		<button @click="toggleTask2">Задача 2</button>
	</div>
	<ZadanineFirst v-if="zadacha1"/>
	<ZadanieSecond v-if="zadacha2"/>
	</div>
</template>

<style scoped>
	button{
		cursor: pointer;
	}

</style>
