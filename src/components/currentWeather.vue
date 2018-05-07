<template>
  <div class="">

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
        props:["currentw"],
        data() {
          return {
            city : this.currentw.city,
            temperature : this.currentw.temperature,
            humidity : this.currentw.humidity,
            pressure : this.currentw.pressure,
            lastupdate : this.currentw.lastupdate.value,
            wind : this.currentw.wind,
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
            var d = new Date(this.city.sun.rise);
            return (d.getHours()+":"+d.getMinutes());
          },
          sunSet(){
            var d = new Date(this.city.sun.set);
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
