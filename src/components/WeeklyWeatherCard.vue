<template>
    <div class="forecast-container">
      <h2>5-Day Forecast for {{ forecast.city.name }}, {{ forecast.city.country }}</h2>
      <div class="forecast-card" v-for="(item, index) in forecast.list" :key="index">
        <div class="date">{{ new Date(item.dt * 1000).toLocaleDateString() }}</div>
        <div class="time">{{ new Date(item.dt * 1000).toLocaleTimeString() }}</div>
        <img :src="`http://openweathermap.org/img/wn/${item.weather[0].icon}.png`" alt="Weather icon">
        <div class="temp">Temp: {{ item.main.temp }}°C</div>
        <div class="description">{{ item.weather[0].description }}</div>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref, onMounted } from 'vue';
  import axios from 'axios';
  
  const baseUrl = 'https://api.openweathermap.org/data/2.5/forecast';
  const apiKey = 'API_KEY'; // Use your actual API key
  const lat = '44.34';
  const lon = '10.99';
  const forecast = ref({ list: [], city: { name: '', country: '' }});
  
  onMounted(async () => {
    try {
      const response = await axios.get(`${baseUrl}?lat=${lat}&lon=${lon}&appid=${apiKey}&units=metric`);
      forecast.value = response.data;
    } catch (error) {
      console.error('Error fetching forecast data:', error);
    }
  });
  </script>
  
  <style scoped>
  .forecast-container {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  
  .forecast-card {
    display: flex;
    align-items: center;
    justify-content: space-around;
    padding: 10px;
    margin: 10px;
    border: 1px solid #ddd;
    border-radius: 8px;
    /* background-color: #f9f9f9; */
    width: 80%;
  }
  
  .forecast-card img {
    width: 50px;
  }
  
  .date, .time, .temp, .description {
    margin: 0 5px;
  }
  </style>
  
