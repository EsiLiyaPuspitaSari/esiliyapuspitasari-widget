<template>
  <div class="weather-widget">
    <h2 class="widget-title">Cuaca</h2>
    <div class="location-input">
      <label class="b11" for="location">Masukan Lokasimu :</label>
      <input type="text" id="location" v-model="location" />
      <button  @click="fetchWeatherData" class="button-primary">Lihat</button>
    </div>
    <div v-if="weatherData" class="weather-data">
      <div class="data-box">
        <p class="location">Lokasi: {{ weatherData.name }}</p>
      </div>
      <div class="data-box">
        <p v-if="weatherData.main" class="temperature">
          Temperatur: {{ weatherData.main.temp }}°C
        </p>
      </div>
      <div class="data-box">
        <p v-if="weatherData.weather" class="description">
          Deskripsi: {{ weatherData.weather[0].description }}
        </p>
      </div>
    </div>
    <p class="tuu" v-else>Mencari Data Cuaca</p>
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
.widget-title{
  display:inline-block;
  border-top-right-radius: 33px;
  border-bottom-left-radius: 33px;
  padding: 11px 19px;
  box-shadow: 0 2px 4px rgba(0, 194, 243, 0.9);
  font-family:Cambria, Cochin, Georgia, Times, 'Times New Roman', serif;
  text-shadow: #c8ff00 0.5px 1px 4px;
  border-bottom-style: outset;
  border-right-style: ridge;
  border-left-style:outset;
  border-top-style:outset;
}
.widget-title {
  margin: 4px 3px 12px;
  color: rgb(0, 0, 0);
}


.tuu {
  display:inline-block;
  background-color: #413f3d;
  padding: 10px 9px;
  border-radius: 4px;
  box-shadow: 0 2px 4px rgba(0, 255, 42, 0.2);
  border-bottom-style: outset;
  border-right-style: ridge;
  border-left-style:outset;
  border-top-style:outset;
  
}

.tuu {
  margin: 4px 3px 12px;
  color: rgb(255, 255, 255);
}


.b11 {
  display:inline-block;
  background-color: rgba(7, 7, 7, 0.7);
  padding: 10px 9px;
  border-radius: 4px;
  box-shadow: 0 1px 4px rgb(5, 92, 19);
  border-style: ridge;
  
}

.b11 {
  
  margin: 4px 3px 12px;
}


.weather-widget {
  border: 1px solid #ccc;
  padding: 20px;
  margin-bottom: 20px;
  border-bottom-left-radius: 33px;
  border-bottom-right-radius: 33px;
  text-align: center;
  background-color: #f2f1ef;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  animation: containerShadowColorChange 5s infinite;
}


@keyframes containerShadowColorChange {
  0% { box-shadow: 0 0 10px green; }
  20% { box-shadow: 0 0 10px yellow; }
  40% { box-shadow: 0 0 10px orange; }
  60% { box-shadow: 0 0 10px red; }
  80% { box-shadow: 0 0 10px blue; }
  100% { box-shadow: 0 0 10px green; }
}





.widget-title {
  margin-top: 0;
  
  font-size: 24px;
}

.location-input {
  margin-bottom: 10px;
}

.location-input label {
  color: #ffffff;
  font-size: 16px;
  
}

.location-input input {
  width: 200px;
  padding: 10px;
  margin-left:12px;
  border:none;
  border-radius: 4px; 
  font-size: 16px;
  background-color: #ffffff;
  box-shadow: #024242 1px 1px 4px;
  color: #000000;
  
}

.button-primary {
  padding: 10px 20px;
  margin: 21px;
  background-color: #3d3f32;
  color: rgb(255, 255, 255);
  border: none;
  border-radius: 4px;
  font-size: 16px;
  cursor: pointer;
  transition: background-color 0.3s ease;
  box-shadow: 0 2px 4px rgba(22, 11, 222, 4);
  border-bottom-style: outset;
  border-right-style: ridge;
  border-left-style:outset;
  border-top-style:outset;
  
  
}

.button-primary:hover {
  background-color: #000000;
  transition: background-color 0.3s ease;
  box-shadow: 0 2px 4px rgba(22, 112, 222, 4);
}

.weather-data {
  margin-top: 10px;
  color: #000000;
}

.data-box {
  background-color: rgba(236, 205, 205, 0.1);
  padding: 10px;
 border-radius: 4px;
  margin-bottom: 10px;
}

.location {
  font-size: 18px;
  font-weight: bold;
}

.temperature {
  font-size: 24px;
  color: #000000;
}

.description {
  font-size: 16px;
}
</style>
