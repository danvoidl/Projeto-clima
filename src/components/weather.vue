<template>
  <div class="weather" :style="cssProps">
    
    <div class="card">
      <div class="search">
        <input
          type="text"
          placeholder="Digite o local aqui"
          class="infoLocal"
        />
        <div class="loupe" @click="getWeatherVoid()">
          <img
            class="loupeSvg"
            src="../assets/loupe.svg"
            style="width: 20px; height: 20px"
          />
        </div>
      </div>

      <h1 class="local">{{ weather.city }} / {{ weather.country }}</h1>

      <div class="temperature">
        <h2>{{ weather.temperature }}ºC</h2>
      </div>

      <div class="variation">
        <p>Min: {{ weather.min }}ºC</p>
        <p>Max: {{ weather.max }}ºC</p>
      </div>

      <p class="description">{{ weather.description }}</p>
    </div>

  </div>
</template>

<script>


export default {
  data() {
    return {
      weather: {},
      cssProps: {
          backgroundImage: `url(${require('@/assets/flor.jpg')})`
        }
    };
  },
  methods: {
    async getWeather(name) {
      let data = await fetch(
        `https://api.openweathermap.org/data/2.5/weather?q=${name}&appid=7f6d644d8eb5540938a11b03526b9fee`
      );
      let weatherData = await data.json();

      let temperature = weatherData.main.temp - 273.15

      let img = temperature < 9 ? `url(${require('@/assets/rain.jpg')})` : `url(${require('@/assets/sunny.jpg')})`

      this.feedArray(weatherData, img);
    },
    feedArray(weatherData, img) {
      this.weather = {
        city: weatherData.name,
        country: weatherData.sys.country,
        temperature: Math.floor(weatherData.main.temp - 273.15),
        min: Math.floor(weatherData.main.temp_min - 273.15),
        max: Math.floor(weatherData.main.temp_max - 273.15),
        description: weatherData.weather[0].description,
      };

      this.cssProps.backgroundImage = img
      
    },
    async getWeatherVoid() {
      let name = document.querySelector(".infoLocal").value.replace(" ", "+");
      await this.getWeather(name);
    },
  },
  async created() {
    this.getWeather("São+paulo");
  },
};
</script>

<style>
*{
  padding: 0;
  margin: 0;
}

.weather {
  height: 100vh;
  width: 100%;
  min-width: 500px;

  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;

  display: grid;
  place-items: center;

  transition: 600ms;
}

.weather img{
  z-index: -1;
  width: 100%;
  height: 100vh;
  object-fit: cover;
}

.search {
  text-align: center;
  margin-top: 1%;
  display: flex;
  justify-content: space-around;
  width: 100%;
  height: 30px;
  position: relative;
}

.search input {
  height: 100%;
  position: absolute;
  padding-left: 10px;
  border: none;
  background-color: rgb(15, 14, 14, 0.6);
  color: white;
  border-radius: 10px;
  outline: none;
}

.search .loupe {
  position: absolute;
  top: 15%;
  right: 20%;
  width: 10%;
  display: grid;
  place-items: center;
  cursor: pointer;

  border-radius: 10px;
  background-color: white 0.6;
}

.card {
  z-index: 1;
  width: 350px;
  height: 500px;
  margin-top: 2%;
  margin: auto;
  display: grid;
  place-items: center;

  border-radius: 5%;
  border: 1px solid rgba(255, 255, 255, 0.2);
  background-color: transparent;
  backdrop-filter: blur(1.5px);
  background-color: rgb(0, 0, 0, 0.35);
  box-shadow: 3px 3px 5px rgb(24, 24, 24, 0.6);
  color: white;

  font-family: "Courgette", cursive;
  font-family: "JetBrains Mono", monospace;
}

.local {
  text-align: center;
  padding: 2%;
}

.temperature {
  width: 200px;
  height: 200px;
  margin: auto;
  position: relative;
  border-radius: 50%;
  border: 1px solid white;
}

.temperature h2 {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  font-size: 35px;
}

.variation {
  width: 70%;
  display: flex;
  justify-content: space-around;
}

.description {
  text-transform: capitalize;
}
</style>