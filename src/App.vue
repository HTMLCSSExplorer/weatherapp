<template>
  <main>
    <!-- Date -->
    <div class="text-center mb-6">
      {{
        new Date().toLocaleDateString('en-us', {
          weekday: 'long',
          year: 'numeric',
          month: 'long',
          day: 'numeric',
        })
      }}
    </div>
    <!-- Search -->
    <div class="container m-auto">
      <SearchField @weatherData="handleWeatherData"></SearchField>
      <div v-if="Object.keys(data.weather).length !==0" >
        <WeatherCard></WeatherCard>
      </div>
    </div>
  </main>
</template>

<script setup>
import { reactive, provide } from 'vue'
import SearchField from './components/SearchField.vue'
import WeatherCard from './components/WeatherCard.vue'
WeatherCard
const data = reactive({
  weather: '',
  forecast: '',
})
const handleWeatherData = (currentWeather, foreCastWeather) => {
  ;(data.weather = currentWeather), (data.forecast = foreCastWeather)
 
}

provide('weatherInfo', data)
</script>

<style>
@import url(https://fonts.googleapis.com/css?family=Poppins:100,100italic,200,200italic,300,300italic,regular,italic,500,500italic,600,600italic,700,700italic,800,800italic,900,900italic);
</style>
