
<script setup lang="ts">import { computed, ref } from 'vue';

interface Props {
    title?: string;
    start: number
}

const props = defineProps<Props>();



const counter = ref(5);


const increase = () => {
    counter.value++;
}

const decrease = () => {
    counter.value--;
}

const squareCounter = computed( () => Math.pow(counter.value, props.start ));

const customTitle = computed( () => props.title || 'Buenas tardes' )

</script>

<template>
    <h2>{{ customTitle }}</h2>
    <p>{{ counter }}<sup>{{ props.start }}</sup> = {{ squareCounter }}</p>

    <div>
        <button @click="increase">+1</button>
        <button @click="decrease">-1</button>
    </div>
</template>


<style scoped>
button {
    background-color: #64B687;
    border-radius: 5px;
    border: 1px solid #5aa67b;
    color: white;
    cursor: pointer;
    margin: 0 5px;
    padding: 5px 15px;
    transition: 0.3s ease-in-out;
}

button:hover {
    background-color: #5aa67b;
    transition: 0.3s ease-in-out;
}

</style>