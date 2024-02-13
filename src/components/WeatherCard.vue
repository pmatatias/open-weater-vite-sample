<template>
    <div class="weather-card" v-if="weather">
      <h2>{{ weather.name }}, {{ weather.sys.country }}</h2>
      <p>{{ weather.weather[0].main }} - {{ weather.weather[0].description }}</p>
      <p>Temperature: {{ weather.main.temp }}°C</p>
      <p>Humidity: {{ weather.main.humidity }}%</p>
    </div>
  </template>
  
  <script setup>
  import { ref, onMounted } from 'vue';
  import axios from 'axios';
  
  const apiKey = 'API_KEY'; // Replace with your OpenWeatherMap API key
  const lat = '44.34'; // Example latitude
  const lon = '10.99'; // Example longitude
  const weather = ref(null);
  
  async function fetchWeather() {
    try {
      const url = `https://api.openweathermap.org/data/2.5/weather?lat=${lat}&lon=${lon}&appid=${apiKey}&units=metric`;
      const { data } = await axios.get(url);
      weather.value = data;
    } catch (error) {
      console.error('Error fetching weather data:', error);
    }
  }
  
  onMounted(fetchWeather);
  </script>
  
  <style scoped>
  .weather-card {
    padding: 20px;
    margin: 20px;
    border: 1px solid #ccc;
    border-radius: 8px;
    width: fit-content;
    /* background-color: #f9f9f9; */
  }
  </style>
  
