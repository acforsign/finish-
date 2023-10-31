<template>
  <div id="app">
  <section class="component-wrapper">
    <PigonDiv class="pigon-container"/>
    <Bod/>
    
  </section>t
  
    
  </div>
</template>

<script>

import PigonDiv from './components/PigonDiv.vue';
import Bod from './components/Bod.vue';


export default {
  name: 'App',
  components: {
    Bod,
    PigonDiv,
  }
}
</script>

<style lang="scss"  scoped>


body{


  background:#2c3e50 ;
  color: #2c3e50;
}


$darkBlue: #0B3A42;
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  background-color: $darkBlue;
  height: 100vh;
  margin: 0;
  box-sizing: border-box;
  
  
}


.component-wrapper{

  width: 100%;
  display: flex;
  flex-direction: column;
  
 
}

.pigon-container{
position: absolute;
left: 15%;


}


</style>
