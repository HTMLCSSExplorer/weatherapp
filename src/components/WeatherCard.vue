<template>
  <div
    class="text-white p-10 rounded-lg shadow-lg gap-6 mb-6 relative overflow-hidden"
    :class="data.weather.current.is_day === 1 ? 'bg-day' : 'bg-night'"
  >
    <!-- Location & time -->
    <div class="mb-2 flex justify-between items-center">
      <div class="flex items-center justify-center gap-2">
        <i class="fa-solid fa-location-dot"></i>
        <h1 class="text-3xl">{{ data.weather.location.name }}</h1>
      </div>
      <div class="flex items-center justify-center gap-2">
        <i class="fa-solid fa-clock"></i>
        <h1 class="text-3xl">{{ data.weather.location.localtime }}</h1>
      </div>
    </div>

    <!-- current weather -->
    <div class="text-center flex-1">
      <img
        :src="data.weather.current.condition.icon"
        alt="icon"
        width="200"
        class="mx-auto -mb-10"
      />
      <h1 class="text-9xl mb-2">{{ Math.round(data.weather.current.temp_c) }}</h1>
      <p class="text-2xl">{{ data.weather.current.condition.text }}</p>
    </div>

    <BorderLine />

    <!-- forecast -->
    <div>
      <!-- Weather daily forecast component goes here -->
      <WeatherForecastDay></WeatherForecastDay>
    </div>

    <!-- info -->
    <Transition>
      <div v-if="infoStat">
        <!-- Weather info component goes here -->

        <WeatherInfo @closeInfo="closeInfo"></WeatherInfo>
      </div>
    </Transition>

    <!-- forecast btn -->
    <div class="flex justify-end items-center gap-1 mt-10">
      <button @click="showWeatherInfo">
        More <i class="fa-solid fa-arrow-right text-sm -mb-px"></i>
      </button>
    </div>
  </div>
</template>

<script setup>
import BorderLine from './BorderLine.vue'
import { inject, ref } from 'vue'
import WeatherForecastDay from './WeatherForecastDay.vue'
import WeatherInfo from './WeatherInfo.vue'
const infoStat = ref(false)
const data = inject('weatherInfo')
console.log(data.weather.current.is_day)

const showWeatherInfo = () => {
  infoStat.value = true
}

const closeInfo = (sate) => {
  sate ? (infoStat.value = false) : ''
}
</script>
<style scoped>
.bg-day {
  background-color: #8ec5fc;
  background-image: linear-gradient(62deg, #8ec5fc 0%, #e0c3fc 100%);
}
.bg-night {
  background-color: #07223d;
  background-image: linear-gradient(62deg, #0a2a4a 0%, #270845 100%);
}

.v-enter-active,
.v-leave-active {
  transition: opacity 0.5s ease;
}

.v-enter-from,
.v-leave-to {
  opacity: 0;
}
</style>
