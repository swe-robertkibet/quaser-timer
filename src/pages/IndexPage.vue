<template>
  <q-page 
      v-touch-pan.vertical.prevent="handlePan"
      class="row items-center justify-evenly text-white">
    <div class="row">
      <q-input
        v-model="data.name"
        input-class="text-center text-h5 text-white"
        color="teal"
        filled
        placeholder="Counter" />
    </div>
    <div class="row full-width items-center">
      <div class="col text-center">
        <q-btn
          round
          size="xl"
          icon="remove" 
          @click="decreaseCounter"
          v-touch-repeat:300:300:300:300:50="decreaseCounter" />
      </div>
      <div class="col text-center text-h2">{{ data.counter }}</div>
      <div class="col text-center">
        <q-btn
          round
          size="xl"
          icon="add"
          @click="increaseCounter"
          v-touch-repeat:300:300:300:300:50="increaseCounter" />
      </div>
    </div>
    <div class="row">
      <q-btn
        round
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
import { watch, reactive } from 'vue';

const data = reactive({
  counter: 0,
  name: ''
})

watch(() => data.counter, (newValue) => {
  console.log('Counter changed:', newValue)
})

const increaseCounter = () => {
  data.counter++
}

const decreaseCounter = () => {
  if (data.counter > 0) data.counter--
}

const resetCounter = () => {
  data.counter = 0
}

const handlePan = (e: { delta: { y: number } }) => {
  if (e.delta.y < 0) {
    increaseCounter()
  } else {
    decreaseCounter()
  }
}
</script>