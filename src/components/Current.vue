<template>
<div v-if="isResponse !== true" id="start">
    <h1 id="title">Weather App</h1>
    <p id="desc">Our weather app is a comprehensive and user-friendly tool that keeps you informed about current and forecasted weather conditions. It provides real-time updates on temperature, precipitation, wind speed, and more, all displayed in an intuitive interface. With personalized location-based forecasts, interactive maps, and customizable notifications, our app ensures you're prepared for any weather situation. Download it today for a smarter way to stay connected to the ever-changing skies.</p>
    <div id="container">
        <button @click="getData" id="Search" for="City">
            <img v-bind:src="require('../assets/Search.png')" alt="">
        </button>
        <input id="City" type="text" v-model="currentInputCity" :placeholder="placeholder">
    </div>
</div>
<div v-if="isResponse === true">
    <div id="current">
        <div id="norm" v-if="clouds < 30 && currentTemp > 18 && currentState !== 'Mist'">
            <button @click="getData" id="Search" for="City">
            <img v-bind:src="require('../assets/Search.png')" alt="">
        </button>
            <div id="data">
                <input id="City" type="text" v-model="currentInputCity" :placeholder="placeholder"> 
                <h1 v-if="isResponse === true">{{ currentTemp }} °</h1>
                <p id="State">{{ currentState }}</p>
            </div>
            <div class="gol"></div>
        </div>
        <div id="frig" v-else-if="currentState === Mist">
            <button @click="getData" id="Search" for="City">
                <img v-bind:src="require('../assets/Search.png')" alt="">
            </button> 
            <div id="data">
                <input id="City" type="text" v-model="currentInputCity" :placeholder="placeholder"> 
                <h1 v-if="isResponse === true">{{ currentTemp }} °</h1>
                <p id="State">{{ currentState }}</p>
            </div>
            <div class="gol"></div>
        </div>
        <div id="zero" v-else-if="currentTemp === 0">
            <button @click="getData" id="Search" for="City">
                <img v-bind:src="require('../assets/Search.png')" alt="">
            </button> 
            <div id="data">
                <input id="City" type="text" v-model="currentInputCity" :placeholder="placeholder"> 
                <h1 v-if="isResponse === true">{{ currentTemp }} °</h1>
                <p id="State">{{ currentState }}</p>
            </div>
            <div class="gol"></div>
        </div>
        <div id="subzero" v-else-if="currentTemp < 0">
            <button @click="getData" id="Search" for="City">
                <img v-bind:src="require('../assets/Search.png')" alt="">
            </button> 
            <div id="data">
                <input id="City" type="text" v-model="currentInputCity" :placeholder="placeholder"> 
                <h1 v-if="isResponse === true">{{ currentTemp }} °</h1>
                <p id="State">{{ currentState }}</p>
            </div>
            <div class="gol"></div>
        </div>
        <div id="frig" v-else="">
            <button @click="getData" id="Search" for="City">
                <img v-bind:src="require('../assets/Search.png')" alt="">
            </button> 
            <div id="data">
                <input id="City" type="text" v-model="currentInputCity" :placeholder="placeholder"> 
                <h1 v-if="isResponse === true">{{ currentTemp }} °</h1>
                <p id="State">{{ currentState }}</p>
            </div>
            <div class="gol"></div>
        </div>
    </div>
</div>
    <div v-if="isResponse === true">
        <div id="forecast-data">
            <h2>Today</h2>
            <h4>{{ currentCity }}</h4>
        </div>
        <div id="forecast">
                <div  class="forecast" id="first">
                <p>{{ hourlyData[0] }} °</p>
                <img v-bind:src="require('../assets/Sunny.png')" v-if="isResponse === true && data.data.forecast.forecastday[0].hour[0].condition.text === 'Sunny'">
                <img v-bind:src="require('../assets/NightClouds.png')" v-else-if="isResponse === true && data.data.forecast.forecastday[0].hour[4].condition.text === 'Partly cloudy' && data.data.forecast.forecastday[0].hour[1].is_day === 1" >
                <img v-bind:src="require('../assets/SunClouds.png')" v-else-if="isResponse === true && data.data.forecast.forecastday[0].hour[0].condition.text === 'Partly cloudy'">
                <img v-bind:src="require('../assets/RainySun.png')" v-else-if="isResponse === true && data.data.forecast.forecastday[0].hour[0].condition.text === 'Patchy rain possible'">
                <img v-bind:src="require('../assets/Sunny.png')" v-else-if="isResponse === true && data.data.forecast.forecastday[0].hour[0].condition.text === 'Clear'">
                <img v-bind:src="require('../assets/RainySun.png')" v-else-if="isResponse === true && data.data.forecast.forecastday[0].hour[0].condition.text === 'Light rain'">
                <img v-bind:src="require('../assets/RainySun.png')" v-else-if="isResponse === true && data.data.forecast.forecastday[0].hour[0].condition.text === 'Light drizzle'">
                <img v-bind:src="require('../assets/RainySun.png')" v-else-if="isResponse === true && data.data.forecast.forecastday[0].hour[0].condition.text === 'Light rain shower'">
                <img v-bind:src="require('../assets/HeavyRain.png')" v-else-if="isResponse === true && data.data.forecast.forecastday[0].hour[0].condition.text === 'Thundery outbreaks possible'">
                <img v-bind:src="require('../assets/RainySun.png')" v-else-if="isResponse === true && data.data.forecast.forecastday[0].hour[0].condition.text === 'Moderate or heavy rain shower'">            
                <img v-bind:src="require('../assets/Cloudy.png')" v-else-if="isResponse === true && data.data.forecast.forecastday[0].hour[0].condition.text === 'Overcast' || data.data.forecast.forecastday[0].hour[0].condition.text === 'Cloudy'">
                <p>{{ hoursForecast[0] }}:00</p>
            </div>
                <div  class="forecast">
                    <p>{{ hourlyData[1] }} °</p>
                    <img v-bind:src="require('../assets/Sunny.png')" v-if="isResponse === true && data.data.forecast.forecastday[0].hour[1].condition.text === 'Sunny'">
                    <img v-bind:src="require('../assets/NightClouds.png')" v-else-if="isResponse === true && data.data.forecast.forecastday[0].hour[4].condition.text === 'Partly cloudy' && data.data.forecast.forecastday[0].hour[1].is_day === 1" >
                    <img v-bind:src="require('../assets/SunClouds.png')" v-else-if="isResponse === true && data.data.forecast.forecastday[0].hour[1].condition.text === 'Partly cloudy'">
                    <img v-bind:src="require('../assets/RainySun.png')" v-else-if="isResponse === true && data.data.forecast.forecastday[0].hour[1].condition.text === 'Patchy rain possible'">
                    <img v-bind:src="require('../assets/Sunny.png')" v-else-if="isResponse === true && data.data.forecast.forecastday[0].hour[1].condition.text === 'Clear'">
                    <img v-bind:src="require('../assets/RainySun.png')" v-else-if="isResponse === true && data.data.forecast.forecastday[0].hour[1].condition.text === 'Light rain'">
                    <img v-bind:src="require('../assets/RainySun.png')" v-else-if="isResponse === true && data.data.forecast.forecastday[0].hour[1].condition.text === 'Light drizzle'">
                    <img v-bind:src="require('../assets/RainySun.png')" v-else-if="isResponse === true && data.data.forecast.forecastday[0].hour[1].condition.text === 'Light rain shower'">
                    <img v-bind:src="require('../assets/HeavyRain.png')" v-else-if="isResponse === true && data.data.forecast.forecastday[0].hour[1].condition.text === 'Thundery outbreaks possible'">
                    <img v-bind:src="require('../assets/RainySun.png')" v-else-if="isResponse === true && data.data.forecast.forecastday[0].hour[1].condition.text === 'Moderate or heavy rain shower'">
                    <img v-bind:src="require('../assets/RainySun.png')" v-else-if="isResponse === true && data.data.forecast.forecastday[0].hour[1].condition.text === 'Mist'">
                    <img v-bind:src="require('../assets/Cloudy.png')" v-else-if="isResponse === true && data.data.forecast.forecastday[0].hour[0].condition.text === 'Overcast' || data.data.forecast.forecastday[0].hour[1].condition.text === 'Cloudy'">
                    <p>{{ hoursForecast[1] }}:00</p>
            </div>
            <div  class="forecast">
                    <p>{{ hourlyData[2] }} °</p>
                    <img v-bind:src="require('../assets/Sunny.png')" v-if="isResponse === true && data.data.forecast.forecastday[0].hour[2].condition.text === 'Sunny'">
                    <img v-bind:src="require('../assets/NightClouds.png')" v-else-if="isResponse === true && data.data.forecast.forecastday[0].hour[4].condition.text === 'Partly cloudy' && data.data.forecast.forecastday[0].hour[2].is_day === 1" >
                    <img v-bind:src="require('../assets/SunClouds.png')" v-else-if="isResponse === true && data.data.forecast.forecastday[0].hour[2].condition.text === 'Partly cloudy'">
                    <img v-bind:src="require('../assets/RainySun.png')" v-else-if="isResponse === true && data.data.forecast.forecastday[0].hour[2].condition.text === 'Patchy rain possible'">
                    <img v-bind:src="require('../assets/Sunny.png')" v-else-if="isResponse === true && data.data.forecast.forecastday[0].hour[2].condition.text === 'Clear'">
                    <img v-bind:src="require('../assets/RainySun.png')" v-else-if="isResponse === true && data.data.forecast.forecastday[0].hour[2].condition.text === 'Light rain'">
                    <img v-bind:src="require('../assets/RainySun.png')" v-else-if="isResponse === true && data.data.forecast.forecastday[0].hour[2].condition.text === 'Light drizzle'">
                    <img v-bind:src="require('../assets/RainySun.png')" v-else-if="isResponse === true && data.data.forecast.forecastday[0].hour[2].condition.text === 'Light rain shower'">
                    <img v-bind:src="require('../assets/HeavyRain.png')" v-else-if="isResponse === true && data.data.forecast.forecastday[0].hour[2].condition.text === 'Thundery outbreaks possible'">
                <img v-bind:src="require('../assets/RainySun.png')" v-else-if="isResponse === true && data.data.forecast.forecastday[0].hour[2].condition.text === 'Moderate or heavy rain shower'">
                <img v-bind:src="require('../assets/RainySun.png')" v-else-if="isResponse === true && data.data.forecast.forecastday[0].hour[2].condition.text === 'Mist'">
                <img v-bind:src="require('../assets/Cloudy.png')" v-else-if="isResponse === true && data.data.forecast.forecastday[0].hour[0].condition.text === 'Overcast' || data.data.forecast.forecastday[0].hour[2].condition.text === 'Cloudy'">
                    <p>{{ hoursForecast[2] }}:00</p>
            </div>
            <div  class="forecast">
                    <p>{{ hourlyData[3] }} °</p>
                    <img v-bind:src="require('../assets/Sunny.png')" v-if="isResponse === true && data.data.forecast.forecastday[0].hour[3].condition.text === 'Sunny'">
                    <img v-bind:src="require('../assets/NightClouds.png')" v-else-if="isResponse === true && data.data.forecast.forecastday[0].hour[4].condition.text === 'Partly cloudy' && data.data.forecast.forecastday[0].hour[3].is_day === 1" >
                    <img v-bind:src="require('../assets/SunClouds.png')" v-else-if="isResponse === true && data.data.forecast.forecastday[0].hour[3].condition.text === 'Partly cloudy'">
                    <img v-bind:src="require('../assets/RainySun.png')" v-else-if="isResponse === true && data.data.forecast.forecastday[0].hour[3].condition.text === 'Patchy rain possible'">
                    <img v-bind:src="require('../assets/Sunny.png')" v-else-if="isResponse === true && data.data.forecast.forecastday[0].hour[3].condition.text === 'Clear'">
                    <img v-bind:src="require('../assets/RainySun.png')" v-else-if="isResponse === true && data.data.forecast.forecastday[0].hour[3].condition.text === 'Light rain'">
                    <img v-bind:src="require('../assets/RainySun.png')" v-else-if="isResponse === true && data.data.forecast.forecastday[0].hour[3].condition.text === 'Light drizzle'">
                    <img v-bind:src="require('../assets/RainySun.png')" v-else-if="isResponse === true && data.data.forecast.forecastday[0].hour[3].condition.text === 'Light rain shower'">
                    <img v-bind:src="require('../assets/HeavyRain.png')" v-else-if="isResponse === true && data.data.forecast.forecastday[0].hour[3].condition.text === 'Thundery outbreaks possible'">
                <img v-bind:src="require('../assets/RainySun.png')" v-else-if="isResponse === true && data.data.forecast.forecastday[0].hour[3].condition.text === 'Moderate or heavy rain shower'">
                <img v-bind:src="require('../assets/RainySun.png')" v-else-if="isResponse === true && data.data.forecast.forecastday[0].hour[3].condition.text === 'Mist'">
                <img v-bind:src="require('../assets/Cloudy.png')" v-else-if="isResponse === true && data.data.forecast.forecastday[0].hour[0].condition.text === 'Overcast' || data.data.forecast.forecastday[0].hour[3].condition.text === 'Cloudy'">
                    <p>{{ hoursForecast[3] }}:00</p>
            </div>
            <div  class="forecast">
            <p>{{ hourlyData[4] }} °</p>
                    <img v-bind:src="require('../assets/Sunny.png')" v-if="isResponse === true && data.data.forecast.forecastday[0].hour[4].condition.text === 'Sunny'">
                    <img v-bind:src="require('../assets/NightClouds.png')" v-else-if="isResponse === true && data.data.forecast.forecastday[0].hour[4].condition.text === 'Partly cloudy' && data.data.forecast.forecastday[0].hour[4].is_day === 1" >
                    <img v-bind:src="require('../assets/SunClouds.png')" v-else-if="isResponse === true && data.data.forecast.forecastday[0].hour[4].condition.text === 'Partly cloudy'" >
                    <img v-bind:src="require('../assets/RainySun.png')" v-else-if="isResponse === true && data.data.forecast.forecastday[0].hour[4].condition.text === 'Patchy rain possible'">
                    <img v-bind:src="require('../assets/Sunny.png')" v-else-if="isResponse === true && data.data.forecast.forecastday[0].hour[4].condition.text === 'Clear'">
                    <img v-bind:src="require('../assets/RainySun.png')" v-else-if="isResponse === true && data.data.forecast.forecastday[0].hour[4].condition.text === 'Light rain'">
                    <img v-bind:src="require('../assets/RainySun.png')" v-else-if="isResponse === true && data.data.forecast.forecastday[0].hour[4].condition.text === 'Light drizzle'">
                    <img v-bind:src="require('../assets/RainySun.png')" v-else-if="isResponse === true && data.data.forecast.forecastday[0].hour[4].condition.text === 'Light rain shower'">
                    <img v-bind:src="require('../assets/HeavyRain.png')" v-else-if="isResponse === true && data.data.forecast.forecastday[0].hour[4].condition.text === 'Thundery outbreaks possible'">
                    <img v-bind:src="require('../assets/RainySun.png')" v-else-if="isResponse === true && data.data.forecast.forecastday[0].hour[4].condition.text === 'Moderate or heavy rain shower'">
                    <img v-bind:src="require('../assets/RainySun.png')" v-else-if="isResponse === true && data.data.forecast.forecastday[0].hour[4].condition.text === 'Mist'">
                    <img v-bind:src="require('../assets/Cloudy.png')" v-else-if="isResponse === true && data.data.forecast.forecastday[0].hour[0].condition.text === 'Overcast' || data.data.forecast.forecastday[0].hour[4].condition.text === 'Cloudy'">
                    <p>{{ hoursForecast[4] }}:00</p>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios';
export default {
    data() {
        return {
            currentTemp:0,
            currentState:'',
            currentCity:'',
            currentInputCity:'',
            placeholder:'Enter city name',
            clouds:0,
            data:{

            },
            hourlyData:[],
            hoursForecast:[],
            lastUpdated:"",
            param:"",
            isPM:false,
            convH:0,
            isResponse:false


        }
    },
    methods: {
        async getData() {
            try {
                this.convH = 0
                const test = await axios.get('http://api.weatherapi.com/v1/forecast.json?key=386ff44423524ec89a2114131232806&q=' + this.currentInputCity + '&days=1&aqi=no&alerts=no');
                this.currentTemp = test.data.current.feelslike_c;
                this.currentState = test.data.current.condition.text;
                this.currentCity = test.data.location.name;
                this.data = test;
                for(let i = 0;i <= 4;i++) {
                    this.hourlyData[i] = this.data.data.forecast.forecastday[0].hour[i].feelslike_c;
                }
                this.lastUpdated = this.data.data.current.last_updated;
                let i = 0;
                while(this.lastUpdated[i] !== " ") {
                    i++;
                }
                this.lastUpdated = this.lastUpdated.substring(i);
                this.param = this.lastUpdated[1] + this.lastUpdated[2];
                console.log(this.data.data);
                if(this.lastUpdated[4] === 3) {
                    convH = convH + 1;
                }

            switch(this.param) {
                case "01":this.convH = this.convH + 1;break;
                case "02":this.convH = this.convH + 2;break;
                case "03":this.convH = this.convH + 3;break;
                case "04":this.convH = this.convH + 4;break;
                case "05":this.convH = this.convH + 5;break;
                case "06":this.convH = this.convH + 6;break;
                case "07":this.convH = this.convH + 7;break;
                case "08":this.convH = this.convH + 8;break;
                case "09":this.convH = this.convH + 9;break;
                case "10":this.convH = this.convH + 10;break;
                case "11":this.convH = this.convH + 11;break;
                case "12":this.convH = this.convH + 12;break;
                case "13":this.convH = this.convH + 13;break;
                case "14":this.convH = this.convH + 14;break;
                case "15":this.convH = this.convH + 15;break;
                case "16":this.convH = this.convH + 16;break;
                case "17":this.convH = this.convH + 17;break;
                case "18":this.convH = this.convH + 18;break;
                case "19":this.convH = this.convH + 19;break;
                case "20":this.convH = this.convH + 20;break;
                case "21":this.convH = this.convH + 21;break;
                case "22":this.convH = this.convH + 22;break;
                case "23":this.convH = this.convH + 23;break;
                case "24":this.convH = this.convH + 24;break;
            
            };
            for(let i = 0;i <= 4;i++) {
                this.convH = this.convH + 1;
                if(this.convH < 25) {
                    this.hoursForecast[i] = this.convH;
                }else{
                    this.convH = 1;
                    this.hoursForecast[i] = this.convH;
                }
            };
            this.isResponse = true;

            } catch(e) {

            };
        }
    }
    //this.data.data.forecast.forecastday[0].hour[0].feelslike_c
}
</script>

<style>
    * {
        font-family: 'Ubuntu', sans-serif;
    }
    #norm {
        background: rgb(2,0,36);
        background: linear-gradient(45deg, rgba(2,0,36,1) 0%, rgba(241,67,97,1) 0%, rgba(238,190,85,1) 100%);
        height:50vh;
        width:100vw;
        display:flex;
        flex-direction: row-reverse;
        justify-content: center;
    }
    h1 {
        margin-top:10vh;
        font-weight: 500;
        font-size:72pt;
        color:#FFFFFF;
    }
    #State {
        margin-top:1vh;
        font-size: 23pt;
        color:#FFFFFF;
    }
    #City {
        width: 100%;
        font-size: 23pt;
        margin-top: 5vh;
        border:none;
        background:transparent;
        text-align:center;
        color:#FFFFFF;
    }
    #City:focus-visible {
        border:none;
        background:transparent;
        outline: none;
        text-align:center;
        color:#FFFFFF;
    }
    #City::placeholder {
        color:#FFFFFF;
    }
    #Search {
        border:none;
        background: transparent;
        height:fit-content;
        width:5vw;
        margin-top: 5vh;
        padding:0;
        margin-left:5vw;
    }
    #data {
        display:flex;
        flex-direction: column;
        align-items: center;
        width: 40vw;
    }
    #frig {
        background: rgb(2,0,36);
        background: linear-gradient(167deg, rgba(2,0,36,1) 0%, rgba(67,132,241,1) 0%, rgba(14,85,110,1) 100%);
        height:50vh;
        width:100vw;
        display:flex;
        flex-direction: row-reverse;
        justify-content: center;
    }
    #zero {
        background: rgb(2,0,36);
        background: linear-gradient(324deg, rgba(2,0,36,1) 0%, rgba(172,185,208,1) 0%, rgba(178,194,199,1) 100%);
        height:50vh;
        width:100vw;
        display:flex;
        flex-direction: row-reverse;
        justify-content: center;
    }
    #subzero {
        background: rgb(2,0,36);
        background: linear-gradient(324deg, rgba(2,0,36,1) 0%, rgba(172,185,208,1) 0%, rgba(178,194,199,1) 100%);
        height:50vh;
        width:100vw;
        display:flex;
        flex-direction: row-reverse;
        justify-content: center;
    }
    .gol {
        min-width: 10vw;
    }
    @media (max-width:750px) {
        #City {
            font-size:17pt;
            
        }
        h1 {
            font-size: 56pt;
        }
        #State {
            font-size: 17pt;
        }
    }
    @media (max-width:400px) {
        #City {
            font-size:14pt;
            
        }
        h1 {
            font-size: 30pt;
        }
        #State {
            font-size: 14pt;
        }
    }
    #barier {
        min-height: 15vh;
    }
    #forecast {
        max-height:50vh;
        overflow-x:auto;
        overflow-y: hidden;
        display:flex;
        max-width:100vw;
        margin-left:5vw;
        margin-right:5vw;
        margin-top:3vh;
    }
    .forecast {
        height:20vh;
        min-width:17vw;
        line-height: 10vh;
        border-radius: 20px;
        display:inline;
        text-align:center;
        /*background: rgb(2,0,36);*/
        margin-left:1vw;
        border:2px solid #000000;
        /*background: linear-gradient(45deg, rgba(2,0,36,1) 0%, rgba(241,67,97,1) 0%, rgba(238,190,85,1) 100%);*/
    }
    h2 {
        align-self: flex-start;
        margin-top:10vh;
        margin-left:5vw;
    }
    #forecast p {
        line-height: 5vh;
    }
    #forecast-data {
        display:flex;
        min-width: 90vw;
        justify-content: space-between;
    }
    #forecast-data h4 {
        margin-top:10vh;
        margin-right: 5vw;
    }
    #first {
        margin-left:0;
    }
    #start {
        min-height: 100vh;
        min-width: 100vw;
        background: url(../assets/Background.png);
        background-size: cover;
        top:0;
        position: fixed;
    }
    #container {
        display: flex;
        flex-direction: row-reverse;
        justify-content: center;
    }
    #Search {
        margin-right:5vw;
    }
    #Search::placeholder {
        color:darkcyan;
    }
    #desc {
        color:#FFFFFF;
        text-align: center;
        padding: 0 20vw;
        padding-top: 10vh;
    }
    @media (max-width:520px) {
        #desc {
            padding:0 10vw;
            padding-top: 10vh;
        }
    }
    #City {
        margin-left: 5vw;
    }
    #title {
        color:#FFFFFF;
        text-align: center;
        padding: 0 20vw;
        font-size: 25pt;
    }
</style>