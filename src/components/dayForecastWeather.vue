<template>
  <div class="col-sm-4">
    <div class="dayname">
      <p class="text-center">{{day.name}}</p>
    </div>
    <div class="row">
      <div class="col-sm-12">
          Hi: <b>{{day.max}}</b>°
        <br>
        Low: <b>{{day.min}}</b>°
      </div>
    </div>
  </div>
</template>

<script>
    export default {
        name: "dayForecastWeather",
        props:["day"],
        data(){
          return {
            temperature : {min : this.day.min, max : this.day.max},
            clouds : {all : 0, unit : "%", value : "clear sky"}
          };
        }
    }
</script>

<style scoped>
.dayname{
  font-weight: bold;
  color: #30aabe;
}
</style>
