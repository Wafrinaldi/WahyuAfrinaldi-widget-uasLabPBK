<template>
    <div class="weather-widget">
        <h2 class="widget-title">Weather Widget</h2>
        <div class="location-input">
            <input type="text" id="location" placeholder="Search Location..." v-model="location" />
            <p></p>
            <button @click="fetchWeatherData" style="background-color: #fa8072;">Get Weather</button>
        </div>
        <div v-if="weatherData" class="weather-data">
            <p class="location">Location: {{ weatherData.name }}</p>
            <p v-if="weatherData.main" class="temperature">
                {{ weatherData.main.temp }}°C
            </p>
            <p v-if="weatherData.weather" class="description">
                Description: {{ weatherData.weather[0].description }}
            </p>
            <p v-if="weatherData.weather" class="additional-info">
                Current weather: <span class="weather-description">{{ weatherData.weather[0].description.toLowerCase()
                }}</span> with a temperature of <span class="temperature-value">{{ weatherData.main.temp }}°C</span>.
            </p>
        </div>
        <p v-else>Loading weather data...</p>
    </div>
</template>
  
<script>
export default {
    data() {
        return {
            location: '',
            weatherData: null
        };
    },
    methods: {
        async fetchWeatherData() {
            try {
                const apiKey = 'b7bfca7b27a3485144fea086c50d09dc';
                const apiUrl = `https://api.openweathermap.org/data/2.5/weather?q=${this.location}&appid=${apiKey}`;

                const response = await fetch(apiUrl);
                const data = await response.json();

                this.weatherData = data;
            } catch (error) {
                console.error('Error fetching weather data:', error);
            }
        }
    }
};
</script>
  
<style scoped>
.weather-widget {
    padding: 20px;
    margin: 100px auto;
    height: 55vh;
    width: 50%;
    text-align: center;
    background-color: rgba(255, 255, 255, 0.2);
    box-shadow: 0px 0px 8px 3px #888888;
    font-family: 'Montserrat', sans-serif;
    border-radius: 5%;
}


.widget-title {
    margin-top: 0;
    color: #fff;
    font-size: 28px;
    font-weight: 300;
}

.location-input {
    margin-bottom: 10px;
}

.location-input input[type="text"] {
    padding: 10px;
    width: 40%;
    border-radius: 15px 0 15px 0;
    font-size: 16px;
    transition: width 1s;
}

.location-input input:focus {
    width: 50%;
    border-radius: 0 15px 0 15px;
    transition: width 1s;
}

.location-input input .location-input button {
    padding: 8px 12px;
    border: none;
    background-color: #fa8072;
    color: #fff;
    font-size: 16px;
    font-weight: bold;
    border-radius: 4px;
    cursor: pointer;
    transition: background-color 0.3s ease;
}

.location-input button:hover {
    background-color: #fa8090;
}

.weather-data {
    margin-top: 10px;
}

.location {
    font-size: 18px;
    font-weight: bold;
}

.temperature {
    font-size: 40px;
    font-weight: bold;
    color: #fa8090;
    margin: 0 auto;
    padding: 50px;
    width: 50%;
    background-color: rgba(255, 255, 255, 0.1);
    border-radius: 15px;
}

.description {
    font-size: 16px;
}

.additional-info {
    font-size: 14px;
    margin-top: 10px;
}

.weather-description {
    font-weight: bold;
}

.temperature-value {
    font-weight: bold;
    color: #fa8090;
}
</style>
  