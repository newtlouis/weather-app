<template>
<div class="weather__box">
    <div class="shadow">
        <input type="text" class="search__box" placeholder="Rechercher une ville .." v-model="query" @keyup.enter="sendLocation"> 
        <div class="weather__info">
        <div class="location">
            <div class="adress">Westhouse</div>
            <div class="date">Today</div>
        </div>
        <div class="weather__physics">
            <div class="temp">20°C</div>
            <div class="weather">Sunny</div>
        </div>
    </div>
    </div>
    
</div>
</template>

<script>
export default {
    name : 'weather',
    data(){
        return {
            api_key :'9ff00bb0cab54b38ed820f677bfb69a4',
            api_url :'http://api.openweathermap.org/data/2.5/',
            query:'',
            weather: {},
        }
    },
    methods:{
        sendLocation(){
            fetch(`${this.api_url}weather?q=${this.query}&units=metric&APPID${this.api_key}`)
            .then(result => {
                console.log(result);
                let res = result.json();
                console.log(res);
                this.weather.name = res.name;
                this.weather.weather = res.weather;
                this.weather.temperatures = res.temperatures;
            })
            .catch(err => console.log(err))
        }
    }
    
}
</script>

<style scoped>

.weather__box{
    width: 300px;
    height: 500px;
    border: solid;
    border-radius: 20px;
    box-shadow: 0 0 1000px 200px rgb(41, 153, 51);
    margin: 20px auto;
    background-image: url('../assets/sunny.jpg');
    background-size: cover;
    background-position: bottom;
    transition: 0.4s;
}

.shadow{
    width: 100%;
    height: 100%;
    background-image: linear-gradient(to bottom, rgba(0,0,0,0.25), rgba(0,0,0,0.75));
    border-radius: 20px;
    padding: 30px;
}

.search__box{
    width: 100%;
    margin: 10px 0;
    padding: 10px;
    border-radius: 0 16px 0 16px;
    box-shadow: 0 0 16px rgba(0,0,0,0.25);

    outline: none;
    appearance: none;
    border: none;
    background: none;
    background-color: rgba(255,255,255,0.5);
    transition: 0.5s;
}

.search__box:focus{
    background-color: rgba(255,255,255,0.75) ;
    box-shadow: 0 0 16px rgba(0,0,0,0.5);
    border-radius: 16px 0 16px 0 ;
}

.adress{
    color: #FFF;
    font-size: 25px;
    font-weight: 500;
    text-align: center;
    text-shadow:1px 3px  rgba(0,0,0,0.25) ;
}

.date{
    color: #FFF;
    font-size: 15px;
    font-weight: 300;
    font-style: italic;
    text-align: center;
    }

.temp{
    padding: 20px;
    margin: 20px auto;
    font-size: 50px;
    font-weight: 900;
    color: #FFF;
    text-align: center;
    text-shadow: 3px 6px rgba(0,0,0,0.25);
    background-color: rgba(255,255,255,0.25);
    box-shadow: 3px 6px rgba(0,0,0,0.25);
    border-radius: 16px;
}

.weather{
    color: #FFF;
    text-align: center;
    font-size: 30px;
    font-weight: 700;
    font-style: italic;
    text-shadow: 3px 6px rgba(0,0,0,0.25);
}

</style>