<template>
  <div id="app" :class=" typeof weather.main != 'undefined' && weather.main.temp > 25 ?'sunny':''">
    <main>
      <div class="search-box">
        <input type="text" class="search" placeholder="Search" v-model="query" @keyup.enter="callWeather"/>
      </div>
      <div class="weather-content" v-if="typeof weather.main != 'undefined' ">
        <div class="location-box">
           <div class="location">{{weather.name}}</div>
           <div class="date">{{setDate()}}</div>
        </div>
         <div class="weather-box">
            <div class="temp"> {{weather.main.temp}}°C</div>
             <div class="weather">{{weather.weather[0].main}}
               
             </div>
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
      api_key: 'b9e11cbd5c8c5e24e1b07e3cd99309d8',
      url: 'https://api.openweathermap.org/data/2.5/',
      query: 'Ha noi',
      weather: {}
    }
  },
  methods:{
      callWeather(){
         
           fetch(`${this.url}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
           .then(res =>{
             return res.json();
           }).then(this.setWeather);
         
      },
      setWeather(rs){
         this.weather = rs;
      },
      setDate(){
        let date = new Date();
        let days = ["Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday","Sunday"];
        let months =["Jan", "Feb", "Mar", "Apr", "May", "Jun", "Jul", "Aug", "Sep", "Oct", "Nov", "Dec"];
        let day = days[date.getDay()];
        let month = months[date.getMonth()];
        let year = date.getFullYear();
        let d = date.getDate();
        return `${day} ${d} ${month} ${year}`;
      }
  }
}
</script>

<style>
  *{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }
  body {
    font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;

  }
  #app{
    background-image: url('./assets/bg.jpg');
    background-position: bottom;
    background-size: cover;
    transition: 0.8s;
  }
  main{
    min-height: 100vh;
    padding: 30px;
    background-image: linear-gradient(to bottom,rgba(0,0,0,0.25),rgba(0,0,0,0.35));
  }
  .search-box{
    width: 90%;
    
  }
  .search{
    width: 100%;
    color: #313131;
    padding: 10px;
    font-size: 20px;
    appearance: none;
    outline: none;
    box-shadow: 0 0 16px rgba(0, 0, 0, 0.25);
    background: none;
    background-color: rgba(255,255,255,0.5);
    border-radius: 20px;
    transition: 0.4s;
  }
  .search:focus{
    background-color: rgba(255,255,255,0.75);
  }
  .weather-content{
    margin-top: 100px;
  }
  .location{
    color: #F0F2FB;
    font-size:32px;
    font-weight: bold;
    line-height: 64px;
    text-align: center;
  }
  .date{
    color: #fff;
    font-size: 24px;
    line-height: 42px;
    text-align: center;
    font-style: italic;
  }
  .weather-box{
    text-align: center;
  }
  .temp{
    margin: 50px 0;
    display: inline-block;
    font-size: 100px;
    color: #F7FFFB;
    background-color: rgba(255,255,255,0.25);
    padding: 10px 25px;
    border-radius: 20px;
    text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
    box-shadow:  8px 8px rgba(0, 0, 0, 0.25);
    font-weight: 900;
  }
  .weather{
    font-size: 50px;
    font-weight: 700;
    color: #fff;
    font-style: italic;
  }
  @media screen and (max-width:660px){
    .temp{
      font-size: 50px;
    }
    .weather{
      font-size: 40px;
    }
  }
  #app.sunny{
      background-image: url('./assets/bg2.jpg');
  }
</style>
