<template>
  <div class="container" id="app">
    <div class="row">
      <div class="col-md-12">
        <h1>Weather Demo</h1>
        <div class="mx-auto">
          <form class=" ">
            <div class="form-group">
              <input type="text" placeholder="your city name" class="border-color" v-model="city">
            </div>
            <div class="form-group">
              <button class="btn btn-outline-info d-block mx-auto" type="button" @click="submit">Find</button>
            </div>
          </form>
        </div>
      </div>
    </div>
    <div class="row">
      <app-city-weather v-if="weatherReceived && forecastReceived" class="col-sm-12"
                        :currentw="currentWeather"
                        :forecastw="forecastWeather"
                        :forecastReceived="forecastReceived">
      </app-city-weather>
    </div>
  </div>
</template>

<script>
  import AppCityWeather from "./components/cityWeather";

  export default {
    name: 'App',
    components : {
      AppCityWeather,
    },
    data: function() {
      return {
        city : "",
        currentWeather : {},
        weatherReceived : false,
        forecastWeather : {},
        forecastReceived : false,
      };
    },
    methods: {
      submit(){
        if (this.city.length<=0)
          return;
        this.weatherReceived = false;
        this.$http.get("api/v1/weather/"+this.city)
          .then(response => {
            return response.json();
          })
          .then(data => {
            this.currentWeather = data.current;;
            this.weatherReceived = true;
          })
          .catch(error => {
            console.log(error.message);
          });

        this.$http.get("api/v1/forecast/"+this.city)
          .then(response => {
            return response.json();
          })
          .then(data => {
            this.forecastWeather = data.weatherdata.forecast.time;
            this.forecastReceived = true;
          })
          .catch(error => {
            console.log(error.message);
          })
      }
    }
  }
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
