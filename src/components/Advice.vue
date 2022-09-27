<script setup>
import { ref, onMounted } from 'vue'
import axios from 'axios'

const id = ref(0)
const advice = ref('')

onMounted(() => {
  reloadAdvice()
})

function reloadAdvice() {
  axios.get('https://api.adviceslip.com/advice/' + Math.floor(Math.random() * 224))
    .then(response => {
      id.value = response.data.slip.id
      advice.value = response.data.slip.advice
    })
    .catch(error => console.log(error))
  
}
</script>

<template>
  <div class="container mx-auto flex items-center justify-center h-screen">
    <div class="card relative bg-slate-700 shadow-sm shadow-slate-700 p-6 rounded-md w-1/3">
      <h1 class="text-sm text-center text-green-500 font-bold">ADVICE #{{ id }}</h1>
      <div class="px-10 py-2">
        <p class="text-xl text-center py-2 text-gray-300">"{{ advice }}"</p>
        <div class="h-3 border-b-2 border-gray-400 text-sm text-center">
            <span class="bg-slate-700 px-5 font-bold text-gray-300" >||</span>
        </div>
        
      </div>
      <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6 bg-green-500 rounded-md cursor-pointer text-slate-800 absolute -bottom-6 left-1/2 transform -translate-x-1/2 -translate-y-1/2" @click="reloadAdvice">
        <path stroke-linecap="round" stroke-linejoin="round" d="M7.5 3.75H6A2.25 2.25 0 003.75 6v1.5M16.5 3.75H18A2.25 2.25 0 0120.25 6v1.5m0 9V18A2.25 2.25 0 0118 20.25h-1.5m-9 0H6A2.25 2.25 0 013.75 18v-1.5M15 12a3 3 0 11-6 0 3 3 0 016 0z" />
      </svg>
    </div>
  </div>
  

</template>

