<template>
    <div id="main">
        <div id="norm" v-if="clouds < 30 && currentTemp > 18 && currentState !== 'Mist'">
            <button @click="getData" id="Search" for="City">
                <img v-bind:src="require('../assets/Search.png')" alt="">
            </button> 
            <div id="data">
                <input id="City" type="text" v-model="currentInputCity" :placeholder="placeholder"> 
                <h1>{{ currentTemp }} °</h1>
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
                <h1>{{ currentTemp }} °</h1>
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
                <h1>{{ currentTemp }} °</h1>
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
                <h1>{{ currentTemp }} °</h1>
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
                <h1>{{ currentTemp }} °</h1>
                <p id="State">{{ currentState }}</p>
            </div>
            <div class="gol"></div>
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
            placeholder:'Enter a city',
            clouds:0
        }
    },
    methods: {
        async getData() {
            try {
                const test = await axios.get('http://api.weatherapi.com/v1/forecast.json?key=386ff44423524ec89a2114131232806&q=' + this.currentInputCity + '&days=1&aqi=no&alerts=no');
                this.currentTemp = test.data.current.feelslike_c;
                this.currentState = test.data.current.condition.text;
                this.currentCity = test.data.location.name;
                console.log(test);
            } catch(e) {
            };
        }
    }
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
        margin-top:10vh;
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
        min-width: 10vh;
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
</style>