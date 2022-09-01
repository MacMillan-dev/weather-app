<template>
  <div class="weatherCard">
    <div class="search">
      <input
        v-model="location"
        type="text"
        class="search-bar"
        placeholder="Enter location"
      />
      <button @click="search">Search</button>
    </div>
  </div>
  <div class="weather-loading" v-if="showCard">
    <h2 class="city">Location: {{cityName}}</h2>
    <div class="flex">
      <img :src="imgUrl" alt="" class="icon" />
      <div class="description">{{description}}</div>
    </div>
    <h2 class="temp">Temp(deg celsius): {{temperature}}</h2>
    <div class="weatherItems">
      <div class="humidity">Humidity: <br>{{humidity}}</div>
      <div class="wind-speed">Wind-speed(knots):<br>
       {{windSpeed}}</div>
    </div>
  </div>
</template>
<script>
import { ref } from "@vue/reactivity";
export default {
  setup() {
    let location = ref("");
    let cityName = ref("")
    let temperature = ref("0");
    let humidity = ref("0");
    let windSpeed = ref("0");
    let apiKey = "7845088629a7abe8771d4553505af431";
    let imgUrl = ref("")
    let description = ref("")
    let showCard = ref(false)

    async function search() {
        await fetch(`https://api.openweathermap.org/data/2.5/weather?q=${location.value}&appid=${apiKey}&units=metric`)
          .then((res) => res.json())
          .then((data) => {
          cityName.value = data.name+","+data.sys.country
          windSpeed.value = data.wind.speed
          humidity.value = data.main.humidity
          temperature.value = data.main.temp
          description.value = data.weather[0].description

          const iconName = data.weather[0].icon
          imgUrl.value = 'http://openweathermap.org/img/w/' + iconName + '.png'
          //console.log(imgUrl.value)
          //console.log(data);
          location.value=''
          })
          .catch((err) => console.log(err));
          showCard.value=true
          //console.log('clicked')
      }

    return { location, apiKey, search, temperature, humidity, windSpeed, imgUrl, cityName, description, showCard };
  },
};
</script>

<style>
input {
  padding: 8px;
  border-radius: 8px;
  border: 2px solid steelblue;
  margin: 15px;
  width: 200px;
  font-size:15px;
}
button {
  border: 1px solid steelblue;
  color: white;
  padding: 6px;
  border-radius: 4px;
  background: steelblue;
  letter-spacing: 2px;
  cursor: pointer;
  font-size:15px;
  }
  button:hover{
    transform: scale(0.98);
  }
.temp{
  padding-top:60px;
}
.weather-loading {
  background-color: lavender;
  max-width: 300px;
  height: 450px;
  border: 0;
  border-radius: 10px;
  flex-direction: column;
  margin: auto;
  overflow: hidden;
  box-shadow: 0 10px 15px rgba(0, 50, 90, 0.8);
}
.weatherItems {
  display: flex;
  column-gap: 100px;
  justify-content: space-between;
  font-weight: bold;
  margin: 70px 10px 0 10px;
}
.flex{
  padding-top:20px;
}
</style>
