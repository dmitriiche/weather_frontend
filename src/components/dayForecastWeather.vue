<template>
  <div class="container">
    Hi: <b>{{temperature.max}}</b>
    <br>
    Low: <b>{{temperature.min}}</b>
  </div>
</template>

<script>
    export default {
        name: "dayForecastWeather",
        data(){
          return {
            temperature : {min : 0, max : 0},
            clouds : {all : 0, unit : "%", value : "clear sky"}
          };
        }
    }
</script>

<style scoped>

</style>
