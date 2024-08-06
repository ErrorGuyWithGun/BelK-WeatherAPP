<template>
    <div
      class=" max-w-96 mb-4 border text-center rounded-md px-4 py-2 bg-slate-300 cursor-pointer flex "
      @click="toggleWeatherDetails"
    >
      <p>{{ weather.datetime }}</p>
      <div class="mx-4">
        <p>Temp: {{ weather.max_temp }}°С - {{ weather.min_temp }}°С</p>
        <div v-if="isExpanded" class="mt-2">
          <p>Wind spd: {{ weather.wind_spd }} m/s</p>
          <p>Average relative humidity: {{ weather.rh }}%</p>
          <p>Wind dir: {{ weather.wind_dir }} degrees ({{ weather.wind_cdir_full }})</p>
        </div>
      </div>
    </div>
  </template>
  
  <script setup lang="ts">
  import { ref,defineProps } from 'vue';
  
  interface WeatherCardProps {
    weather: {
      max_temp: number;
      min_temp: number;
      wind_spd: number;
      datetime: string;
      rh: number;
      wind_dir: string;
      wind_cdir_full: string;
    };
  }
  
  defineProps<WeatherCardProps>();
  
  const isExpanded = ref(false);
  
  function toggleWeatherDetails() {
    isExpanded.value = !isExpanded.value;
  }

  </script>