<template>
    <div class="container">

      <div class="row">
        <h1>{{cityName}}, {{country}}</h1>
      </div>
      <div class="row">
        <b>Current conditions</b>
      </div>
      <app-current-weather class="col-sm-4" :currentw="currentw"></app-current-weather>
      <app-forecast-weather v-if="forecastReceived" :forecastw="forecastw"></app-forecast-weather>
    </div>
</template>

<script>
  import AppCurrentWeather from "./currentWeather";
  import AppForecastWeather from "./forecatsWeather";

    export default {
        name: "cityWeather",
        components : {
          AppCurrentWeather,
          AppForecastWeather
        },
        props:["currentw", "forecastw", "forecastReceived"],
        data(){
          return {
            cityName : this.currentw.city.name,
            country : this.currentw.city.country
          };
        }
        // created() {
        //   console.log("cityWeather component created!");
        //   console.log(this.currentw);
        //   console.log(this.forecastw);
        //   console.log(this.forecastReceived);
        // }
    }
</script>

<style scoped>

</style>
