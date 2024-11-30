<template>
  <div>
    <!-- search field -->
    <form @input="getQuery">
      <div class="bg-white border border-indigo-600/30 rounded-lg shadow-lg flex items-center">
        <i class="fa-solid fa-magnifying-glass p-2 text-indigo-600"></i>
        <input
          type="text"
          placeholder="Search for a place"
          class="rounded-r-lg p-2 border-0 outline-0 focus:ring-2 focus:ring-indigo-600 ring-inset w-full"
          v-model.trim="searchTerm.query"
        />
      </div>
    </form>
    <!-- search suggestions -->
    <div class="bg-white my-2 rounded-lg shadow-lg">
      <div v-for="result in searchTerm.results" :key="result.id">
        <button
          class="px-3 my-2 hover:text-indigo-600 hover:font-bold w-full text-left"
          @click="getWeatherData(result.id)"
        >
          {{ result.name }}, {{ result.region }}, {{ result.country }}
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
import axios from 'axios'
import { reactive } from 'vue'

const searchTerm = reactive({
  query: '',
  results: null,
  timeOut: null,
  weatherData: '',
  forecastData: '',
})
const emit = defineEmits(['weather-data'])
const getQuery = async () => {
  clearTimeout(searchTerm.timeOut)
  searchTerm.timeOut = setTimeout(async () => {
    if (searchTerm.query !== '') {
      await axios
        .get(
          `http://api.weatherapi.com/v1/search.json?key=402165f15f1142a194930802240509&q=${searchTerm.query}`,
        )
        .then((res) => {
          searchTerm.results = res.data
        })
    }
  }, 10)
}

const getWeatherData = async (cityId) => {
  await axios(
    `http://api.weatherapi.com/v1/current.json?key=402165f15f1142a194930802240509&q=id:${cityId}`,
  ).then((res) => (searchTerm.weatherData = res.data))
  await getForecastData(cityId)
  emit('weather-data', searchTerm.weatherData, searchTerm.forecastData)
  resetInput()
}
const getForecastData = async (cityId) => [
  await axios(
    `http://api.weatherapi.com/v1/forecast.json?key=402165f15f1142a194930802240509&q=id:${cityId}`,
  ).then((res) => (searchTerm.forecastData = res.data)),
]
const resetInput = () => {
  searchTerm.query = ''
  searchTerm.results = []
}
</script>
