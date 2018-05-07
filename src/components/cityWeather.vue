<template>
    <div class="container">

      <div class="row">
        <h1>{{cityName}}, {{country}}</h1>
      </div>
      <div class="row">
        <div class="col-sm-4 text-left app-header">
          <b>Current conditions</b>
        </div>
        <div class="col-sm-8 text-left app-header">
          <b>3 day outlook</b>
        </div>
      </div>
      <div class="row">
        <app-current-weather class="col-sm-4" :currentw="currentw"></app-current-weather>
        <app-forecast-weather class="col-sm-8" v-if="forecastReceived" :forecastw="forecastw"></app-forecast-weather>
      </div>
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
    }
</script>

<style scoped>
  .app-header{
    font-size: 1.2em;
    line-height: 1.1em;
    font-weight: 700;
    padding: 4px 8px;
    background-color: #b3dfe7;
  },
  [class*="col-"] {
    background-clip: padding-box;
    border: 5px solid transparent;
  }
</style>
