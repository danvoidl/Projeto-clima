<template>
<link href="https://fonts.googleapis.com/css2?family=Courgette&family=JetBrains+Mono:wght@600&display=swap" rel="stylesheet">

  <div id="container-weather"> 
  <!--  <div class="title">
        <h1> Weather</h1>
        <p> 
            Made using the 
            <a href="https://openweathermap.org/">OpenweatherMap</a> 
            data and <strong>Vue</strong>.js
        </p>
    </div>-->
      <Weather></Weather>
  </div>
</template>

<script>
import Weather from './components/weather'

export default {
    data(){
        return {
            
        }
    },
    components: { Weather }
}
</script>

<style>

.title{
    text-align: center;
    padding-top: 2%;
}

a{
    text-decoration: none;
}

strong{
    color: #41b883;
}
</style>