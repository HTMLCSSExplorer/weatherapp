<template>
  <div
    class="absolute bg-white/80 backdrop-blur-sm text-slate-900 inset-x-0 bottom-0 rounded-t-lg p-8"
  >
    <!-- Close button -->
    <div class="flex justify-end mb-10">
      <button class="p-1">
        <i class="fa-solid fa-xmark text-xl" @click="closeInfo"></i>
      </button>
    </div>

    <div class="flex items-center justify-between gap-6 mb-20">
      <!-- Wind speed -->
      <div class="text-center flex-1">
        <i class="fa-solid fa-wind mb text-2xl"></i>
        <p class="text-xl font-bold">{{ injectedData.weather.current.wind_kph }} km/h</p>
        <p>wind</p>
      </div>
      <!-- Humidity level -->
      <div class="text-center flex-1">
        <i class="fa-solid fa-droplet mb text-2xl"></i>
        <p class="text-xl font-bold">{{ injectedData.weather.current.humidity }} %</p>
        <p>humidity</p>
      </div>
      <!-- Precipitation -->
      <div class="text-center flex-1">
        <i class="fa-solid fa-umbrella mb text-2xl"></i>
        <p class="text-xl font-bold">{{ injectedData.weather.current.precip_mm }}</p>
        <p>precipitation</p>
      </div>
    </div>
    <div class="flex items-center justify-between gap-6 mb-10">
      <!-- Wind direction -->
      <div class="text-center flex-1">
        <i class="fa-solid fa-fan mb text-2xl"></i>
        <p class="text-xl font-bold">{{ injectedData.weather.current.wind_dir }}</p>
        <p>direction</p>
      </div>
      <!-- Feels like -->
      <div class="text-center flex-1">
        <i class="fa-solid fa-temperature-half mb text-2xl"></i>
        <p class="text-xl font-bold">{{ Math.round(injectedData.weather.current.feelslike_c) }}</p>
        <p>Feels</p>
      </div>
      <!-- UV -->
      <div class="text-center flex-1">
        <i class="fa-solid fa-sun mb text-2xl"></i>
        <p class="text-xl font-bold">{{ injectedData.weather.current.uv }}</p>
        <p>UV index</p>
      </div>
    </div>
    <!-- Last update and delete -->
    <div class="flex justify-between items-center">
      <h3 class="text-slate-900/50">last update:{{ injectedData.weather.current.last_updated }}</h3>
      <button>
        <i class="fa-solid fa-trash"></i>
      </button>
    </div>
  </div>
</template>

<script setup>
import { inject, reactive } from 'vue'
const injectedData = inject('weatherInfo')

const emit = defineEmits(['closeInfo'])
const state = reactive({ isOpen: true })

const closeInfo = () => {
  emit('closeInfo', state.isOpen)
}
</script>
