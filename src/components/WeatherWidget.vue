<template>
  <div class="weather-widget">
    <h2>Weather Widget</h2>
    <div v-if="isLoading">
      Loading weather data...
    </div>
    <div v-else>
      <p>Current temperature: {{ temperature }}°C</p>
      <p>Weather condition: {{ condition }}</p>
      <p>Location: {{ location }}</p>
    </div>
    <div v-if="!isLoading">
      <form @submit.prevent="submitWeatherData">
        <label for="temperature">Temperature (°C):</label>
        <input type="number" id="temperature" v-model="userTemperature" required>
        <label for="condition">Weather condition:</label>
        <input type="text" id="condition" v-model="userCondition" required>
        <label for="location">Location:</label>
        <input type="text" id="location" v-model="userLocation" required>
        <button type="submit">Submit</button>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: 'WeatherWidget',
  data() {
    return {
      isLoading: true,
      temperature: null,
      condition: null,
      location: null,
      userTemperature: null,
      userCondition: null,
      userLocation: null
    };
  },
  mounted() {
    // Simulating an API call to fetch weather data
    setTimeout(() => {
      this.isLoading = false;
      this.temperature = 25;
      this.condition = 'Sunny';
      this.location = 'Your City';
    }, 2000);
  },
  methods: {
    submitWeatherData() {
      this.temperature = this.userTemperature;
      this.condition = this.userCondition;
      this.location = this.userLocation;
    }
  }
};
</script>

<style scoped>
.weather-widget {
  border: 1px solid #ccc;
  padding: 20px;
  margin-bottom: 20px;
}

form label {
  display: block;
  margin-bottom: 5px;
}

form input {
  margin-bottom: 10px;
  width: 100%;
  padding: 5px;
}

form button {
  padding: 5px 10px;
  background-color: #000000;
  border: none;
  cursor: pointer;
}

form button:hover {
  background-color: #aaa;
}
</style>
