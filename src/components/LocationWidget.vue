<template>
    <div class="location-widget">
        <h2>Your Location</h2>
        <div v-if="latitude && longitude">
            <p>Latitude: {{ latitude }}</p>
            <p>Longitude: {{ longitude }}</p>
        </div>
        <div v-else>
            <p>Finding your location...</p>
        </div>

        <div class="location-input">
            <label for="latitude">Latitude:</label>
            <input type="text" id="latitude" placeholder="First Koordinat..." v-model="inputLatitude" />
        </div>
        <div class="location-input">
            <label for="longitude">Longitude:</label>
            <input type="text" id="longitude" placeholder="Second Koordinat..." v-model="inputLongitude" />
        </div>

        <button @click="fetchLocationDetails">Find Location Details</button>

        <div v-if="foundLocation">
            <h3>Location Details</h3>
            <p>{{ foundLocation.components.country }}</p>
            <p>{{ foundLocation.components.city }}</p>
            <p>{{ foundLocation.components.street }}</p>
            <p>Postal Code: {{ foundLocation.components.postcode }}</p>
        </div>
    </div>
</template>
  
<script>
export default {
    data() {
        return {
            latitude: null,
            longitude: null,
            inputLatitude: '',
            inputLongitude: '',
            foundLocation: null,
        };
    },
    mounted() {
        if (navigator.geolocation) {
            navigator.geolocation.getCurrentPosition(this.getPosition);
        }
    },
    methods: {
        getPosition(position) {
            this.latitude = position.coords.latitude;
            this.longitude = position.coords.longitude;
        },
        async fetchLocationDetails() {
            try {
                const apiKey = '92591005a7b94008909d59a64b6d2a49';
                const latitude = this.inputLatitude || this.latitude;
                const longitude = this.inputLongitude || this.longitude;
                const apiUrl = `https://api.opencagedata.com/geocode/v1/json?q=${encodeURIComponent(
                    latitude + ',' + longitude
                )}&key=${apiKey}`;

                const response = await fetch(apiUrl);
                const data = await response.json();

                if (data.results && data.results.length > 0) {
                    const location = data.results[0];
                    this.foundLocation = location;
                    console.log('Location:', location);
                    // Lakukan sesuatu dengan data lokasi yang ditemukan
                }
            } catch (error) {
                console.error('Error fetching location data:', error);
            }
        },
    },
};
</script>
  
<style scoped>
.location-widget {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    text-align: center;
    border-radius: 5%;
    margin: 100px auto;
    height: 55vh;
    width: 50%;
    text-align: center;
    background-color: rgba(255, 255, 255, 0.2);
    box-shadow: 0px 0px 8px 3px #888888;
}

.location-widget h2 {
    color: #fff;
    font-size: 30px;
    font-weight: 300;
    margin-bottom: 20px;
}

.location-widget p {
    color: #fff;
}

.location-input {
    margin-top: 20px;
}

.location-input label {
    display: block;
    margin-bottom: 5px;
    color: #fff;
    font-size: 16px;
}

.location-input input {
    width: 200px;
    padding: 10px;
    margin-right: 10px;
    border: 1px solid #ccc;
    border-radius: 4px;
    font-size: 16px;
}

.location-input button {
    padding: 10px 20px;
    background-color: #4caf50;
    color: white;
    border: none;
    border-radius: 4px;
    font-size: 16px;
    cursor: pointer;
    transition: background-color 0.3s ease;
    margin-top: 10px;
}

.location-input button:hover {
    background-color: #45a049;
}

.location-input button:disabled {
    background-color: #ccc;
    color: #999;
    cursor: not-allowed;
}

.location-details {
    margin-top: 20px;
    text-align: left;
}

.location-details h3 {
    margin-bottom: 10px;
    color: #fff;
    font-size: 18px;
}

.location-details p {
    margin: 5px 0;
    color: #fff;
}

.error-message {
    color: red;
    margin-top: 10px;
}

/* Penambahan gaya CSS hingga 100 baris */
.location-widget:before {
    content: "";
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;

    z-index: -1;
    border-radius: 8px;
}
</style>