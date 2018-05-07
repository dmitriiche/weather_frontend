<template>
    <div class="row">
      <app-day-forecast-weather v-for="day in dayForecaComponents" :day="day" :key="day.dayname"></app-day-forecast-weather>
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
              minList.push(Math.round(dayObj[key].temperature.min));
              maxList.push(Math.round(dayObj[key].temperature.max));
            }
            var max = Math.max(...maxList);
            var min = Math.min(...minList);

            return {min: min, max : max};
          }
          var weekday = new Array(7);
          weekday[0] =  "Sunday";
          weekday[1] = "Monday";
          weekday[2] = "Tuesday";
          weekday[3] = "Wednesday";
          weekday[4] = "Thursday";
          weekday[5] = "Friday";
          weekday[6] = "Saturday";

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
          todayTemp.name = "Today";
          this.dayForecaComponents.push(todayTemp);

          var tommorowTemp = getMinMax(tommorowForecast);
          tommorowTemp.name = "Tommorow";
          this.dayForecaComponents.push(tommorowTemp);

          var dayaftertomorrowTemp = getMinMax(dayAfterTomorrowForecast);
          dayaftertomorrowTemp.name = weekday[dayaftertomorrow.getDay()];
          this.dayForecaComponents.push(dayaftertomorrowTemp);
        }
    }
</script>

<style scoped>

</style>
