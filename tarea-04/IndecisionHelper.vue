
<script setup lang="ts">
import { ref, watch } from 'vue';

const question = ref();
const img = ref<string>();
const answer = ref<string | null>( null );

const isValidQuestion = ref(false);

interface Respuesta {
    answer: string;
    forced: boolean;
    image:  string;
}


const getAnswer = async() => {

    answer.value = 'Pensando...';

    const resp: Respuesta = await fetch('https://yesno.wtf/api')
        .then( r => r.json() )
    
    answer.value = resp.answer;

    img.value = resp.image;
   
}

watch( question, (value ) => {

    isValidQuestion.value = false;
    
    if( !value.includes('?') ) return;

    isValidQuestion.value = true;

    getAnswer();
});

</script>

<template>

    <img v-if="img" :src="img" alt="bg">

    <div class="bg-dark"></div>

    <div class="indecision-container">
    
        <input
          type="text"
          placeholder="Hazme una pregunta"
          v-model="question">

          <p>Recuerda terminar con un signo de (?)</p>

          <div v-if="isValidQuestion">
            <h2>{{ question }}</h2>

            <!-- yes no => Sí! - No! -->
            <h1>{{ answer }}</h1>
          </div>
    </div>

</template>


<style scoped>

    img, .bg-dark {
        height: 100vh;
        left: 0px;
        max-height: 100%;
        max-width: 100%;
        position: fixed;
        top: 0px;
        width: 100vw;
    }

    .bg-dark {
        background-color: rgba(0, 0, 0, 0.4);
    }

    .indecision-container {
        position: relative;
        z-index: 99;
    }
    
    input {
        width: 250px;
        padding: 10px 15px;
        border-radius: 5px;
        border: none;
    }
    input:focus {
        outline: none;
    }

    p {
        color: white;
        font-size: 20px;
        margin-top: 0px;
    }

    h1, h2 {
        color: white;
    }
    
    h2 {
        margin-top: 150px;
    }

</style>