<template>
     <div id="app" :class = "typeof (weather.main) != 'undefined' && weather.main.temp < 16 ? 'cold' : 'warm'" >
          <main>
               <div class="search-box">
                    <input
                         type="text"
                         name="search"
                         class="search-bar"
                         placeholder="Seach the name of a city to know the weather"
                         v-model="query"
                         @keypress="fetchweather"
                    />
               </div>

               <div class="weather-wrap" v-if="typeof(weather.main) != 'undefined'">
                    <div class="location-box">
                         <div class="location">{{weather.name}}, {{weather.sys.country}}</div>
                         <div class="date">{{dateBuilder()}}</div>
                    </div>
                    <div class="weather-box">
                        <div class="temp">{{Math.round(weather.main.temp)}}&#176;C</div>
                        <div class="weather">{{weather.weather[0].main}}</div>

                    </div>
               </div>
               <div class="not-found" v-else-if="weather.cod == 404">City Not Found!</div>
          </main>
     </div>
</template>

<script>
export default {
     name: "app",
     data: function() {
          return {
               api_key: "8d3c190147cc82e7dcb0d3050a911d26",
               url_base: "https://api.openweathermap.org/data/2.5/",
                query: '',
                weather: {}
          }
     },
     methods:{
       fetchweather (e){
         if(e.key == "Enter"){
           fetch(`${this.url_base}weather?q=${this.query}&units=metric&appid=${this.api_key}`).
           then(response=>{
             return response.json();
           }).then(this.setResults);
         }
       },
       setResults(results){
         this.weather = results;
         console.log(results)
       },
       dateBuilder(){
         let date = new Date();
         let months =["January", "February", "March", "April", "May", "June", "July", "August", "September", "November", "December"]
         let days= [
           "Sunday",
           "Monday",
           "Tuesday",
           "Wednesday",
           "Thursday",
           "Friday",
           "Saturday"
         ]
         return `${days[date.getDay()]}, ${date.getDate()} ${months[date.getMonth()]},  ${date.getFullYear()}`
       }
     } 
};
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@300;600&display=swap');
*,
::after,
::before {
     margin: 0;
     padding: 0;
     box-sizing: border-box;
}
html,
body {
     font-family: "Montserrat", sans-serif;
     font-size: 65%;
     font-weight: 300;
}

#app {
  background-image: url("https://wallpaper.dog/large/5532051.jpg");
     background-size: cover;
     background-position: bottom;
     transition: 0.5s;
}
#app.warm{
  background-image: url("https://cdn.hipwallpaper.com/i/51/20/Al0PqL.jpg");
}

#app.cold{
  background-image: url('https://c4.wallpaperflare.com/wallpaper/799/452/950/night-snow-mountains-wallpaper-preview.jpg');
}

main {
     min-height: 100vh;
     min-width: 100vw;
     overflow: hidden;
     padding: 35px;
     background-image: linear-gradient(
          to bottom,
          rgba(0, 0, 0, 0.25),
          rgba(0, 0, 0, 0.75)
     );
     text-align: center;
}

.search-box .search-bar {
     display: block;
     width: 90%;
     padding: 15px;
     font-size: 2rem;

     appearance: none;
     border: none;
     outline: none;
     background: none;

     box-shadow: 0px 0px 8px rgba(0, 0, 0, 0.25);
     background-color: rgba(255, 255, 255, 0.5);
     border-radius: 10px;
     transition: 0.4s;
}

.search-bar:focus {
     box-shadow: 0px 0px 8px rgba(0, 0, 0, 0.5);
     background-color: rgba(255, 255, 255, 0.8);
}

/*
               <div class="weather-wrap">
                    <div class="location-box">
                         <div class="location">Northampton, UK</div>
                         <div class="date">Monday 20 January, 2020</div>
                    </div>
                    <div class="weather-box">
                        <div class="weather">Rain</div>
                        <div class="temp">9&#176;C </div>
                    </div>
               </div>
*/

.location-box .location{
  margin-top: 8rem;
  color: white;
  font-size: 3.2rem;
  font-weight: 600;
  text-shadow: 1px 3px rgba(0, 0, 0, .25)
}

.location-box .date{
  font-size: 1.8rem;
  color: white;
  margin-top: 10px;
}

.weather-box{
  color: white;
  height: 15rem;
  width: 15rem;
  margin: 3rem auto;
}
.weather-box .temp{
  font-size: 4.2rem;
  padding: 2rem;
}
.weather-box .weather{
  font-size: 2.2rem;
}
.not-found{
  color: white;
  font-size: 2.4rem;
  margin-top: 2rem;
}
</style>
