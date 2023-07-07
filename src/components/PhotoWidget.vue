<template>
  <div class="photo-widget">
      <h1 class="ket1">Pintasan Foto</h1>
    <div class="image-container">
      <img :src="currentPhoto" :alt="currentPhoto" :style="{ width: '1000px', height: 'auto' }" />
    </div>
    <div class="controls-foto">
      <button class="button-tertiary" @click="kembaliKeBeranda">Kembali ke Beranda</button>
      <button class="button-tertiary" @click="prevPhoto">Sebelumnya</button>
      <button class="button-tertiary" @click="nextPhoto">Selanjutnya</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      photos: [require('../assets/11.jpg'),require('../assets/12.jpg'),require('../assets/13.jpg'),require('../assets/3.jpg'),require('../assets/2.jpg'),require('../assets/4.jpg'),require('../assets/14.jpg'),require('../assets/13.jpg'),require('../assets/15.png'),require('../assets/16.jpg'),require('../assets/5.jpg')],
      currentIndex: 0,
    };
  },
  computed: {
    currentPhoto() {
      return this.photos[this.currentIndex];
    },
  },
  methods: {
    kembaliKeBeranda() {
      this.$router.push('/cuaca')
    },
    prevPhoto() {
      if (this.currentIndex > 0) {
        this.currentIndex--;
      } else {
        this.currentIndex = this.photos.length - 1;
      }
    },
    nextPhoto() {
      if (this.currentIndex < this.photos.length - 1) {
        this.currentIndex++;
      } else {
        this.currentIndex = 0;
      }
    },
  },
};
</script>

<style scoped>

.image-container {
  width: 1000px; /* Atur lebar yang diinginkan */
  height: 700px; /* Atur tinggi yang diinginkan */
  display: flex;
  justify-content: center;
  align-items: center;
  overflow: hidden;
} 

.image-container img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}
.ket1 {
  font-weight: bold;
  margin-top: 1px;
  margin-bottom: 12px;
  color: rgb(197, 31, 31);
  font-family:'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  text-shadow: 2px 2px 4px rgba(243, 238, 238, 0.5);
  font-style: italic;
  text-shadow: #fdddae 1px 1px 5px;
  padding: 10px 66px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.6);
  color: rgb(7, 7, 7);
  border-bottom-style: outset;
  border-right-style: ridge;
  border-left-style:outset;
  border-top-style:outset;

}

.photo-widget {
  margin: 1px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  background-color: rgb(232, 254, 255);
  border-top-right-radius: 40px;
  border-bottom-left-radius: 40px;
  padding: 22px;
  
}

.image-container {
  margin-bottom: 20px;
  border: 1px solid rgb(240, 252, 188); 
  padding: 5px;
  display: flex;
  justify-content: center;
  border-radius: 4px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1), 0 5px 15px rgba(0, 0, 0, 0.1), 0 10px 30px rgba(0, 0, 0, 0.1);
}
.image-container img {
  max-width: 100%;
  max-height: 100%;
  border-radius: 4px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.7);
  
}

.controls-foto {
  display: flex;
  justify-content: center;
  margin-top: 20px;
 
}

.controls-foto button {
  padding: 10px 20px;
  margin: 4px 9px;
  font-size: 23px;
  border-radius: 4px;
  border: none;
  cursor: pointer;
  transition: all 0.3s ease;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 2);
  background-color: #4d4d4d;
  color: rgb(229, 255, 0);
  font-family:Cambria, Cochin, Georgia, Times, 'Times New Roman', serif;
  text-decoration: double;
  animation: containerShadowColorChange 5s infinite;
}

@keyframes containerShadowColorChange {
  100% { box-shadow: 0 0 10px rgb(200, 255, 0); }
  20% { box-shadow: 0 0 10px rgb(0, 255, 255); }
  40% { box-shadow: 0 0 10px rgb(0, 162, 255); }
  60% { box-shadow: 0 0 10px red; }
  80% { box-shadow: 0 0 10px blue; }
  100% { box-shadow: 0 0 10px rgb(0, 255, 0); }
}





.controls-foto button:hover {
  transform: translateY(-2px);
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
}

.controls-foto button:active {
  transform: translateY(0);
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
}
</style>