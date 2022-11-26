<template>
  <div id="App">
      <main>
          <div class="search-box">
            <input 
                 name="" 
                 id="" 
                 type="text" 
                 class="search-bar"
                 v-model="query"


              />
          </div>

          {{ query }}

          <div class="weather-wrap">
            <div class="location-box">
                <div class="location">Auckalnd, New Zealand</div>
                <div class="date">10 nov 2022</div>
            </div>
            <div class="weather-box">
                <div class="temp">18°c</div>
                <div class="weather-image">
                </div>
                <div class="weather">cloudy</div>
                <div class="weather-description">broken clouds</div>
            </div>
          </div>
      </main>
  </div>
</template>


<script>

export default {
  name: 'App',
  data() {
    return {
        api_key: '1bd3f4a8f0486884f6783704a0b9ac2a',
        url_base: 'https://api.openweathermap.org/data/2.5/',
        query: '',
        weather: {}
    }
  },

  methods: {

    fetch_weather(e) {
      if (e.key === "Enter") {
        fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
        .then(res => {
              return res.json();
              }).then(this.setResults);

            }
      
        },
        setResults(results) {
          this.weather = results;
        },
        dataBuilder() {
            let d = new DataTransfer();
            let months = ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"]
            let days = ["Sunday", "Saturday", "Friday", "Thursday", "Wednesday", "Tuesday", "Monday"]
            let day = days[d.getDay()];
            let date = d.getDate();
            let month = months[d.getMonth()];
            let year = d.getFullYear();
            return `${day} ${date} ${month} ${year}`;

        }

      }
    }

  


</script>


<style>

    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      font-family: 'montserrat', sans-serif;
    }

    #app {
      background-image: url("assets/cool-bg.png");
      background-size: cover;
      background-position: bottom;
      transition: 0.4s;
    }

    /* background  lowering the brightness of the background image*/

    main {
      min-height: 100vh;
      padding: 25px;
      background-image: linear-gradient(to bottom, rgba(0,0,0, 0.25), rgba(0,0,0, 0.75)); 
    
    }

    /* search box display */

    .search-box {
      width: 100%;
      margin-bottom: 30px;
    }

    /* style search box, starting from appearance to outline is to remove the shadow. color is to add in color */

    .search-box .search-bar {
      display: block;
      width: 100%;
      padding: 15px;
      color: #313131;
      font-size: 20px;
      box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.25);

      appearance: none;
      border: none;
      background: none;
      outline: none;

      background-color: rgba(255, 255, 255, 0.5);
      border-radius: 10px 10px 10px 10px;
      transition: 0.4s;
    }

    .search-box .search-bar:focus {
      background-color: rgba(255, 255, 255, 0.75);
      box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.25);
      border-radius: 6px 0px 16px 0px;
    }

    /* location */

    .location-box .location {
      color: #FFFFFF;
      font-size: 32px;
      font-weight: 500;
      text-align: center;
      text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
    }

    .location-box .date {
      color: #FFFFFF;
      font-size: 20px;
      font-weight: 300;
      font-style: itatlic;
      text-align: center;
    }

    .weather-box {
      text-align: center;
    }

    /* create for temp */

    .weather-box .temp {
      display: inline-block;
      padding: 10px 25px;
      color: #FFFFFF;
      font-size: 102px;
      font-weight: 900;

      text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
      background-color: rgba(255, 255, 255, 0.25);
      border-radius: 16px;
      margin: 30px 0px;


      box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
    }

    .weather-box .weather {
      color: #FFFFFF;
      font-size: 35px;
      font-weight: 300;
      font-style: italic;
      text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
    }

    .weather-box .weather-description {
      color: #FFFFFF;
      font-size: 10px;
      font-weight: 300;
      font-style: italic;
    }

    .weather-box .weather-image {
      position: center;
    }

</style>