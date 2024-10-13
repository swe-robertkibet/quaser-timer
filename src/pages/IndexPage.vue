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

// Imports
import { watch, reactive, onMounted } from 'vue';
import { useQuasar } from 'quasar'

// Quasar
const $q = useQuasar()

// Define the shape of the data
interface SavedData {
  counter: number;
  name: string;
}

// Reactive data object
const data = reactive<SavedData>({
  counter: 0,
  name: ''
})

// Load saved data from localStorage when app starts
onMounted(() => {
  const savedData = $q.localStorage.getItem('data')

  if (savedData && typeof savedData === 'object') {
    // Ensure savedData has counter and name properties
    data.counter = (savedData as SavedData).counter ?? 0
    data.name = (savedData as SavedData).name ?? ''
  }
})

// Watch for changes in the counter and name, and store them in localStorage
watch([() => data.counter, () => data.name], () => {
  $q.localStorage.set('data', { counter: data.counter, name: data.name })
})

// Counter Methods
const increaseCounter = () => {
  data.counter++
}

const decreaseCounter = () => {
  if (data.counter > 0) data.counter--
}

const resetCounter = () => {
  data.counter = 0
}

// Handle swipe up/down gesture to increase/decrease the counter
const handlePan = (e: { delta?: { x?: number; y?: number } }) => {
  if (e.delta?.y && e.delta.y < 0) {
    increaseCounter()
  } else {
    decreaseCounter()
  }
}

</script>
