<template>
    <div id="weather">
        <h3><strong>Local Weather Report</strong></h3>
        <input type="text" placeholder="Enter city"  v-model="city" @keyup.enter="getWeather">
         <input type="text" placeholder="Enter country" v-model="country" @keyup.enter="getWeather">
        <h4>Tempature: <strong>{{ Math.round(tempature)}}°F</strong></h4>
        <h4>Current Conditions: <strong>{{ conditions }}</strong></h4>
    </div>
</template>

<script>
import axios from 'axios'

  export default {
        name: 'ShowWeather',
        data() {
            return {
                city: '',
                country: '',
                tempature: '',
                conditions: '',
                weatherInfo: {}
            }
        },
        methods: {
            getWeather() {
                axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city},${this.country}&units=imperial&appid=2e475ecda4c3e1d6ad7fea3fb9217fc6`)
            .then(response => (
                this.city = response.data.name,
                this.country = response.data.sys.country,
                this.tempature = response.data.main.temp,
                this.conditions = response.data.weather[0].description,
                console.log(response)
            ))
            },
            }
        }
</script>

<style>
#weather {
  padding-top: 5px;
  margin: auto;
  width: 500px;
  text-align: center;
  border: 1px solid black;
}

@media (max-width: 580px) {
    #weather {
        width: 300px;
    }
}
</style>