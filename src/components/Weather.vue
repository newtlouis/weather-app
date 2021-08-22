<template>
<div class="weather__box" :class="{warm : temperature > 16}">
    <div class="shadow">
        <div class="erreur"></div>
        <input type="text" class="search__box" placeholder="Rechercher une ville .." v-model="query" @keyup.enter="sendLocation"> 
        <div class="weather__info">
        <div class="location">
            <div class="adress">{{name}}</div>
            <div class="date">{{getDate}}</div>
        </div>
        <div class="weather__physics">
            <div class="temp">{{temperature}}°C</div>
            <div class="weather">{{weather}}</div>
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
            name : "Westhouse",
            weather : "Ensoleillé",
            temperature : 25
        }
    },
    computed: {
        getDate(){
            let d = new Date();
            let days = ["lundi", "mardi","mercredi","jeudi","vendredi","samedi","dimanche"]
            let months = ["janvier","février","mars","avril","mai","juin","juillet","août","septembre","octobre","novembre","décembre"]
            let date = days[d.getDay()] +" "+ d.getDate() +" "+ months[d.getMonth()] +" "+ d.getUTCFullYear()
            return date
        }
    }
    ,
    methods:{
        sendLocation(){
            fetch(`http://api.openweathermap.org/data/2.5/weather?q=${this.query}&appid=${this.api_key}&lang=fr`)
            .then(result => {return result.json()})
            .then(this.setResults)
            .catch(err => {
                document.getElementsByClassName("erreur")[0].innerHTML = "Ville inconnue"
                console.log(err)
                })

        },
        setResults(results){
            document.getElementsByClassName("erreur")[0].innerHTML = ""
            this.name = results.name;
            this.weather = results.weather[0].description;
            this.temperature = Math.round(results.main.temp -272.15)
        },
 
    }
    
}
</script>

<style scoped>

.weather__box{
    width: 300px;
    height: 500px;
    border: solid;
    border-radius: 20px;
    box-shadow: 10px 10px  0px rgb(53, 137, 206);
    margin: 20px auto;
    background-image: url('../assets/cold.jpg');
    background-size: cover;
    background-position: bottom;
    transition: 0.4s;
}

.warm{
    background-image: url('../assets/sunny.jpg');
    box-shadow: 10px 10px  0px rgb(212, 64, 5);


}

.shadow{
    width: 100%;
    height: 100%;
    background-image: linear-gradient(to bottom, rgba(0,0,0,0.25), rgba(0,0,0,0.75));
    border-radius: 20px;
    padding: 30px;
}

.erreur{
    color: rgb(247, 111, 111);
    font-weight: 800;
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