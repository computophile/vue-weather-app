<template>
     <div id="app">
          <main>
               <div class="search-box">
                    <input
                         type="text"
                         name="search"
                         class="search-bar"
                         placeholder="Search"
                         v-model="query"
                         @keypress="fetchweather"
                    />
               </div>

               <div class="weather-wrap">
                    <div class="location-box">
                         <div class="location">Northampton, UK</div>
                         <div class="date">Monday 20 January, 2020</div>
                    </div>
                    <div class="weather-box">
                        <div class="temp">9&#176;C </div>
                        <div class="weather">Rain</div>

                    </div>
               </div>
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
           fetch(`${this.api_base}weather?q=${this.query}&appid=${this.api_key}`).
           then(response=>{
             return response.json();
           }).then(this.setResults);
         }
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
     background-image: url("https://cdn.hipwallpaper.com/i/51/20/Al0PqL.jpg");
     background-size: cover;
     background-position: bottom;
     transition: 0.5s;
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
</style>
