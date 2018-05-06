<template>
  <div class="cotainer">

    <div class="row">
      <div class="col-sm-6">
        <span class="temperature" :class="[temperatureClass]">
          {{temperature.value}} °C
        </span>
        <br>
        {{wind.speed.value}} m/s
        <div class="col-sm-12 updatedDate text-left">
          As of {{updateDate}}
        </div>

      </div>
      <div class="col-sm-6 text-left">
        Barometer: <b>{{pressure.value}} {{pressure.unit}}</b> <br>
        Humidity: <b>{{humidity.value}}%</b><br>
        <br>
        Sun rise: <b>{{sunRise}}</b><br>
        Sun set: <b>{{sunSet}}</b>
      </div>
    </div>
  </div>
</template>

<script>

    export default {
        name: "currentWeather",
        data() {
          return {
            cityName : "Castle Rock",
            country : "US",
            temperature : {min : 0, max : 0, value : 0},
            humidity : { unit : "%", value : 100},
            pressure : {unit : "hPa", value : 600},
            lastupdate : "2018-05-05T09:20:00",
            wind : {gusts : "", speed : {name : "Calm", value : 1.5}},
            direction : {code : "SSW", name : "South-southwest", value : 200},
            sun : {set : "2018-05-05T19:03:44", rise : "2018-05-05T01:28:27"}
          };
        },
        computed : {
          temperatureClass() {
            return this.temperature.value >= 0 ? "positiveTemp" : "negativeTemp";
          },
          updateDate(){
            var d = new Date(this.lastupdate);
            return (d.getDate() + "/" + (d.getMonth()+1) + " " + d.getHours()+":"+d.getMinutes());

          },
          sunRise(){
            var d = new Date(this.sun.rise);
            return (d.getHours()+":"+d.getMinutes());
          },
          sunSet(){
            var d = new Date(this.sun.set);
            return (d.getHours()+":"+d.getMinutes());
          }

        }
    }
</script>

<style scoped>
  .temperature{
    font-size: x-large;
    font-weight: bold;
  }
  .negativeTemp{
    color: cornflowerblue;
  }
  .positiveTemp{
    color: #e3303d;
  }
  .updatedDate{
     position: absolute;
     bottom: 0;
     left: 0;
  }
</style>
