<template>
<link href="https://fonts.googleapis.com/css2?family=Courgette&family=JetBrains+Mono:wght@600&display=swap" rel="stylesheet">

  <div id="container-weather"> 
 <div class="title">
        <h1> Weather</h1>
        <p> 
            Made using the 
            <a href="https://openweathermap.org/">OpenweatherMap</a> 
            data and <strong>Vue</strong>.js
        </p>
    </div>
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

#container-weather{
    width: 100%;
    height: 100%;
}

.title{
    position: absolute;
    left: 50%;
    top: 5%;
    color: white;
    transform: translate(-50%, -50%);
    text-align: center;
    padding-top: 2%;
    font-family: "Courgette", cursive;
    font-family: "JetBrains Mono", monospace;
    text-shadow: 2px 2px 2px black;
}

a{
    text-decoration: none;
}

strong{
    color: #41b883;
}
</style>