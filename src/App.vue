<template>
  <div id="app">
    <main>
      <div class="search_box">
        <input type="text" class="search_bar" placeholder="search..." v-model="query" @keypress="fetchWeather">
      </div>
      <div class="weather_wrap"  v-if="typeof weather.main!= 'undefined'">
        <div class="location_box">
          <div class="location">{{weather.name}},{{weather.sys.country}}</div>
          <div class="date">{{dateSec()}}</div>
        </div>
        <div class="weather_box">
          <div class="temp">{{Math.round(weather.main.temp)}}°c</div>
          <div class="weather">{{weather.weather[0].main}}</div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>

export default {
  name: 'App',
  data(){
    return{
      api_key: '4aa3725a391e77d79c3a15a904a3666b',
      url:'https://api.openweathermap.org/data/2.5/',
      query:'',
      weather:{}
    }
  },
  methods:{
    fetchWeather(e){
      if(e.key == "Enter"){
        fetch(`${this.url}weather?q=${this.query}&unit=metric&APPID=${this.api_key}`)
        .then(res=>{
          return res.json();
        }).then(this.setresult)
      }
    },
    setresult(results){
      this.weather=results;
    },
    dateSec(){
          let d = new Date();
          let months=["January","February","March","April","May","June","July","August","September","October","November","December"];
          let days=["Sunday","Saturday","Friday","Thursday","Wednesday","Tuesday","Monday"];

          let day = days[d.getDay()];
          let date = d.getDate();
          let month = months[d.getMonth()];
          let year = d.getFullYear();
          return  `${day} ${date} ${month} ${year}`;

    }
  
  }

}
</script>

<style>
*{
  margin:0;
  padding: 0;
  box-sizing: border-box;
  font-family:'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif ;
}
body{

}
#app {
  background-image: url(./assets/cold.jpg);
  background-size: cover;
  background-position:bottom ;
}
/* #app.hot{
   background-image: url(./assets/hot.jpg);
} */
main{
min-height: 100vh;
padding: 25px;
background: linear-gradient(to bottom ,rgba(0,0,0,0.5),rgba(0,0,0,0.5));

}
.search_box{
  width: 40%;
  margin-bottom: 60px;
  
}
.search_box .search_bar{
  width: 100%;
  display: inline;
  padding: 12px;
  border: none;
  outline: none;
  appearance: none;
  background: #fff;
  background-color: rgba(255,255,255,0.4);
  position: relative;
  color: #fff;
  font-size: 2em;
  left: 55vh;
  border-radius: 10px;
}
.location_box .location{
  color: #fff;
  font-size: 2.3em;
  text-align: center;
  letter-spacing: 2px;
}
.location_box .date{
  color: #fff;
  font-size: 1.4em;
  text-align: center;
  letter-spacing: 2px;
}
.weather_box{
text-align: center;
}
.weather_box .temp{
  display: inline-block;
  padding: 10px 20px;
  font-size: 7em;
  /* background-color: #fff;
  background-color: rgba(255,255,255,0.5); */
  border-radius: 10px;
  color: #fff;
  margin-top: 20px;
  box-shadow: 3px 6px rgba(0,0,0,0.25);
}
.weather_box .weather{
  font-size: 3em;
  color: #fff;
  margin-top: 20px;
}
</style>
