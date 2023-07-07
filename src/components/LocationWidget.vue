<template>
  <div class="location-widget">
    <div class="location-header">
      <h2>Lokasi Kamu</h2>
    </div>
    <div class="location-content">
      <div v-if="latitude && longitude" class="location-info">
        <p >Garis Lintang : {{ latitude }}</p>
        <p >Garis Bujur : {{ longitude }}</p>
      </div>
      <div v-else class="location-info">
        <p class="ss1">Cari Alamat Kamu</p>
      </div>

      <div class="location-input">
        <div class="input-field">
          <label class="p1" for="latitude">Garis Lintang:</label>
          <input type="text" id="latitude" v-model="inputLatitude" />
        </div>
        <div class="input-field">
          <label class="p1" for="longitude">Garis Bujur:</label>
          <input type="text" id="longitude" v-model="inputLongitude" />
        </div>
      </div>

      <button @click="fetchLocationDetails" class="button-primary">Cari Detail Lokasi Kamu</button>

      <div v-if="foundLocation" class="location-details">
        <h3>Detail Lokasi</h3>
        <p>{{ foundLocation.components.country }}</p>
        <p>{{ foundLocation.components.city }}</p>
        <p>{{ foundLocation.components.street }}</p>
        <p>Kode Pos: {{ foundLocation.components.postcode }}</p>
      </div>
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
          // Do something with the found location data
        }
      } catch (error) {
        console.error('Error fetching location data:', error);
      }
    },
  },
};
</script>

<style scoped>
.ss1{
  color: #1d8e96;
  font-family:Georgia, 'Times New Roman', Times, serif;
}
.p1{
  display:inline-block;
  background-color: rgba(162, 0, 255, 0.1);
  padding: 10px 9px;
  margin: 12px;
  border-radius: 4px;
  box-shadow: 0 2px 4px rgba(247, 0, 227, 0.4);
  color: rgb(252, 252, 252);
  border-bottom-style: outset;
  border-right-style: ridge;
  border-left-style:outset;
  border-top-style:outset;
  
}
.location-widget {
  border: 1px solid #ccc;
  padding: 20px;
  margin-bottom: 20px;
  background-color: #c7bb9938;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.location-header {
  text-align: center;
  background-color: #fff8b7;
  box-shadow: #000000 01px 1px 4px;
  color: rgb(0, 0, 0);
  padding: 10px;
  border-top-left-radius: 8px;
  border-top-right-radius: 8px;
  
}

.location-content {
  padding: 20px;
}

.location-info {
  margin-bottom: 20px;
  font-size: larger;
  font-family:Cambria, Cochin, Georgia, Times, 'Times New Roman', serif;
  color: #000000;
  background-color: #ffffe5;
  border: 1px solid #ccc;
  padding: 10px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  border-bottom-left-radius: 23px;
  border-bottom-right-radius: 23px;
  
}

.location-input {
  display:flex;
  justify-content: center;
  align-items: center;
  margin-top: 20px;
  background-color: rgba(221, 238, 217, 0.719);
  padding: 4px 9px ;
  border-radius: 4px;
  box-shadow: 0 2px 4px rgba(119, 119, 119, 0.2);
  color: rgb(0, 0, 0);
  background-color: #fbfcdc;

}


.input-field {
  margin-right: 10px;
}

.input-field label {
  color: #333;
  font-size: 16px;
  margin-bottom: 5px;
}

.input-field input {
  width: 200px;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
  font-size: 16px;
  
}

.button-primary {
  font-family:Cambria, Cochin, Georgia, Times, 'Times New Roman', serif;
  font-style: italic;
  padding: 10px 20px;
  background-color: #ccebf7;
  box-shadow: #76c4e9 1px 1px 2px;
  color: rgb(0, 0, 0);
  border: none;
  margin:12px;
  border-radius: 4px;
  font-size: 16px;
  cursor: pointer;
  transition: background-color 0.3s ease;
  border-bottom-style: outset;
  border-right-style: ridge;
  border-left-style:outset;
  border-top-style:outset;
}

.button-primary:hover {
  background-color: #76c4e9;
}

button:disabled {
  background-color: #ccc;
  color: #999;
  cursor: not-allowed;
}

.button-primary:active {
  transform: translateY(0);
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
}

.location-details {
  margin-top: 20px;
  
  background-color: #fff;
  border: 1px solid #ccc;
  padding: 10px;
  border-radius: 4px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.location-details h3 {
  margin: 0 0 10px;
  color: #333;
  font-size: 18px;
}

.location-details p {
  margin: 5px 0;
  color: #666;
}

.error-message {
  color: red;
  margin-top: 10px;
}


</style>
