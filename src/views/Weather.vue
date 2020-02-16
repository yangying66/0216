<template>
    <div class="about">
        <h1>現在の天気</h1>
        <div id="btn">
            <button @click="showWeather(0)">今日</button>
            <button @click="showWeather(8)">明日</button>
            <button @click="showWeather(16)">明後日</button>
        </div>
        <select v-model="selectValue" >
            <option disabled value="">都市を選択ください。</option>
            <option value="Sapporo">札幌</option>
            <option value="Sendai">仙台</option>
            <option value="Tokyo">東京</option>
        </select>
            <p class="weather_city">{{ city }}</p>
            <p class="weather_city">気温{{ temp }}</p>
            <p v-if="condition.main == 'Rain'">雨<br><img src="../img/雨.jpg" alt=""></p>
            <p v-else-if="condition.main == 'Clouds'">曇り<br><img src="../img/曇り.jpg" alt=""></p>
            <p v-else-if="condition.main == 'Clear'">晴れ<br><img src="../img/晴れ.jpg" alt=""></p>
            <p v-else-if="condition.main == 'Snow'">雪<br><img src="../img/雪.jpg" alt=""></p>
            <p v-else>それ以外</p>     
    </div>
</template>

<script>
    export default{
        data(){
            return {
                day:'0',
                city:'',
                temp:'',
                condition:{
                    main:''
                }
    
            }
        },
            methods:{
           showWeather(day){
           console.log(this.selectValue)
           let apiURL = 'https://api.openweathermap.org/data/2.5/forecast?q=' + this.selectValue + '&appid=c6be84c77f58bbbef4ec233b3a0284bc'
           this.axios.get(apiURL).then(function(response){
           this.city = response.data.list[day].name
           this.temp = response.data.list[day].main.temp
           this.condition = response.data.list[day].weather[0]
           console.log(this.condition)
        }.bind(this)).catch(function(error){
           console.log(error)
            })
        } 
    }
}
 
</script>

<style>
#btn{
margin: 0 auto;

}
button{
    background-color: #f44336;
    border: none;
    color: white;
    padding: 12px 32px;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    font-size: 16px;
    margin: 4px 6px;
    cursor: pointer;
    border-radius: 5px 5px 5px 5px;
}
select{
    margin: 20px 0;
    margin: 20px 0;
    border-radius: 5px 5px 5px 5px;
    height: 30px;
    width: 173px;
    border-style: solid;
    border-width: medium;
    border-color:#f44336;
}
img{
   max-width: 700px;
}
</style>