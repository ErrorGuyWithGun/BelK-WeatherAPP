<template>
  <div>
    <TheHeading/>
    <div class="container mx-auto">
      <div class="flex justify-center">
        <BaseInput
          v-model="city"
          placeholder="Enter your city"
          @keyup.enter="fetchWeather"
          @clear-messages="clearMessages"/>
        <BaseButton 
          @click="fetchWeather" 
          textbutton="Show" />
      </div>
        <p v-if="error" class=" text-red-500 font-bold text-center">{{ error }}</p>
        <p class="mb-4 mt-4" v-if="weatherData && weatherData.city_name">City: {{ weatherData.city_name }}</p> 
          <TheWeatherCard
            v-for="weather in weatherData?.data"
            :key="weather.datetime"
            :weather="weather"/>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted} from 'vue';
import TheHeading from './components/TheHeading.vue';
import BaseButton from '@/components/BaseButton.vue';
import BaseInput from '@/components/BaseInput.vue';
import TheWeatherCard from '@/components/TheWaetherCard.vue';

interface WeatherData {
  city_name: string;
  data: {
    max_temp: number;
    min_temp: number;
    wind_spd: number;
    datetime: string;
    rh: number;
    wind_dir: string;
    wind_cdir_full: string;
  }[];
}

const weatherData = ref<WeatherData | null>(null);
const city = ref('');
const error = ref('');

const fetchWeather = async () => {
  try {
    const response = await fetch(
      `https://api.weatherbit.io/v2.0/forecast/daily?city=${city.value}&days=3&key=03656894f15d421a8751922653040f3a&lang=ru&include=minutely`
    );
    const data: WeatherData = await response.json();
    weatherData.value = data;
    console.log(data);
  } catch (e) {
    console.error('Error:', e);
    error.value = 'Error fetching weather data';
  }
};

function clearMessages() {
  error.value = '';
}

onMounted(() => {
  fetchWeather();
});
</script>