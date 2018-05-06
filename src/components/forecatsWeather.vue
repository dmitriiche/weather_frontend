<template>
    <div class="container">
      <!--<app-day-forecast-weather></app-day-forecast-weather>-->
      <app-day-forecast-weather v-for="day in dayForecaComponents" :day="day" :key="day"></app-day-forecast-weather>
      <!--<app-quote  v-for="quote in quotes" :message="quote"></app-quote>-->
    </div>
</template>

<script>
    import AppDayForecastWeather from "./dayForecastWeather";

    export default {
        name : "forecatsWeather",
        components : {
          AppDayForecastWeather
        },
        props : ["forecastw"],
        data() {
          return {
            dayForecaComponents : []
          };
        },
        created() {
          // Function parse forecast object and return min max temperature for a day
          // Because of openweathermap free version not provide daily forecast.
          function getMinMax(dayObj)
          {
            var minList = [];
            var maxList = [];

            for (let key in dayObj)
            {
              minList.push(dayObj[key].temperature.min);
              maxList.push(dayObj[key].temperature.max);
            }
            var max = Math.max(...maxList);
            var min = Math.min(...minList);

            return {min: min, max : max};
          }

          var today = new Date(Date.now());
          var tommorow = new Date(Date.now());
          tommorow.setDate(tommorow.getDate() + 1);
          var dayaftertomorrow = new Date(Date.now());
          dayaftertomorrow.setDate(dayaftertomorrow.getDate() + 2);

          var todayForecast = [], tommorowForecast = [], dayAfterTomorrowForecast = [];

          for (let key in this.forecastw)
          {
            let date = new Date(this.forecastw[key].from);
            switch (date.getDate()){
              case today.getDate():
                todayForecast.push(this.forecastw[key])
                break;
              case tommorow.getDate():
                tommorowForecast.push(this.forecastw[key])
                break;
              case dayaftertomorrow.getDate():
                dayAfterTomorrowForecast.push(this.forecastw[key])
                break;
            }
          }
          var todayTemp = getMinMax(todayForecast);
          var tommorowTemp = getMinMax(tommorowForecast);
          var dayaftertomorrowTemp = getMinMax(dayAfterTomorrowForecast);


          console.log(todayForecast);
          console.log(tommorowForecast);
          console.log(dayAfterTomorrowForecast);
          console.log(todayTemp);
          console.log(tommorowTemp);
          console.log(dayaftertomorrowTemp);
        }
    }
</script>

<style scoped>

</style>
