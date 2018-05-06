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
              <button class="btn btn-outline-info d-block mx-auto" @click="submit">Find</button>
            </div>
          </form>
        </div>
      </div>
    </div>
    <div class="row">
      <app-city-weather class="col-sm-12"></app-city-weather>
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
        city: ""
      };
    },
    methods: {
      submit(){
        if (this.city.length<=0)
          return;
        this.$http.get("api/v1/weather/"+this.city)
          .then(response => {
            console.log(response.json());
            return response.json();
          })
          .then(data => {
            console.log(data);
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
