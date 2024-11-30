<template>
  <div class="mb-2 flex items-center justify-between">
    <table class="w-full">
      <tr>
        <!-- day of the week -->
        <td class="w-1/3">
          {{
            new Date().toLocaleDateString('en-us', {
              weekday: 'long',
            })
          }}
        </td>

        <!-- icon -->
        <td class="w-1/3">
          <img
            :src="weatherForecats.forecast.forecast.forecastday[0].day.condition.icon"
            alt="icon"
            width="30"
            class="mx-auto"
          />
        </td>

        <!-- high/low temp -->
        <td class="w-1/3 text-right">
          {{ Math.round(weatherForecats.forecast.forecast.forecastday[0].day.maxtemp_c) }}/
          {{ Math.round(weatherForecats.forecast.forecast.forecastday[0].day.mintemp_c) }}
        </td>
      </tr>
    </table>
  </div>
</template>

<script setup>
import { inject } from 'vue'
const weatherForecats = inject('weatherInfo')
</script>
