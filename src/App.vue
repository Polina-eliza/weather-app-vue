


<template>
  <div class="app-container">
    <header>
      <h2 class="app-header">Weather App</h2>
    </header>
    <main>
      <div class="input-container">
        <input type="text" name="city-input" id="cityInput" v-model="cityName" />
        <button @click="getWeather">Search</button>
      </div>
      
      <div class="weather-container">
        <h2 class="city-name">{{ cityName }}</h2>
        <p class="weather-temperature"> {{ weatherTemp }}</p>
      </div>
      <p class="error-message">{{ error }}</p>
    </main>
  </div>
</template>


<script>
import axios from "axios";

export default {
  data() {
    return {
      cityName: '',
      weather: null,
      error: '',
      weatherTemp: '',  
      windSpeed: ''   
    };
  },

  methods: {
    async getWeather() {
      try {
        console.log(this.cityName)
        const response = await axios.get(`https://api.open-meteo.com/v1/forecast?city=${this.cityName}&current_weather=true&hourly=temperature_2m,relativehumidity_2m,windspeed_10m`);
        
        
        this.weather = response.data;
        
        console.log(this.weather);
        
        this.weatherTemp = this.weather.current_weather.temperature;
      } catch (error) {
        this.error = error.response.data;
        console.log("Error:", error);
      }
    }
  }
};
</script>


<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: "Arial";
}

.app-container {
  margin: 100px 200px;
}

button {
  margin-left: 10px;
  margin-top: 20px;
}

.city-name {
  margin: 20px 0;
}

.weather-container p {
  margin-top: 10px;
}




</style>
