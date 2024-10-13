<template>
  <q-page class="row items-center justify-evenly text-white">
    <div class="row" >
      <q-input
      v-model="data.name"
      input-class="text-center text-h5 text-white" 
      color="teal"
      filled 
      placeholder="Counter" />
    </div>
    <div class="row full-width items-center">
      <div class="col text-center">
        <q-btn round 
        @click="decreaseCounter"
        size="xl"
        icon="remove" />
      </div>
      <div class="col text-center text-h2">{{ data.counter }}</div>
      <div class="col text-center">
        <q-btn round 
        @click="increaseCounter"
        size="xl"
        icon="add" />
      </div>

    </div>
    <div class="row">
        <q-btn round 
        @click="resetCounter"
        size="xl"
        icon="restart_alt" />
    </div>
  </q-page>
</template>

<style scoped>
.q-page {
  max-width: 700px;
  margin: 0 auto;
}
</style>



<script setup lang="ts">


// Imports
import { reactive } from 'vue'

// Data
const data = reactive({
  counter: 0,
  name: ''
})

// Counter Methods

const increaseCounter = () => {
  data.counter++
}

const decreaseCounter = () => {
  if(data.counter > 0 ) data.counter--
}

const resetCounter = () => {
  if(data.counter > 0 ) data.counter=0
}



</script>
