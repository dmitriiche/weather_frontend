<template>
    <div class="container">

      <div class="row">
        <h1>{{cityName}}, {{country}}</h1>
      </div>
      <div class="row">
        <b>Current conditions</b>
      </div>
      <app-current-weather class="col-sm-6"></app-current-weather>
    </div>
</template>

<script>
  import AppCurrentWeather from "./currentWeather";

    export default {
        name: "cityWeather",
        components : {
          AppCurrentWeather
        },
        data(){
          return {
            cityName : "Castle Rock",
            country : "US",
          };
        }
    }
</script>

<style scoped>

</style>
