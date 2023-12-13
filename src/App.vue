<template>
  <div class="app">
    <h2>Pomodoro</h2>
    <h3>Press start to begin</h3>
    <div class="container">
      <h1>{{ formattedTime(time) }}</h1>
      <h3 @click="startTime">START</h3>
    </div>
  </div>

</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';


export default defineComponent({
  name: 'App',
  components: {},
  setup(){
    const time= ref(1500)
    const interval= ref<number|undefined>(undefined)

    const deduceTime=() =>{
      if(time.value>0){
        time.value--
        clearInterval(interval.value)
        
      }
      // else if(time.value===0){
      //   console.log("hello");
        
      //   clearInterval(interval.value)
      //   // notifSound()
      //   time.value= 300
      // }
      
    }
    const startTime=() =>{
      interval.value= setInterval(deduceTime, 1000)

    }
    
     //F:\Web_ Development\Vue_Firebase\pomorodoapp\sound\notif01.mp3
    // const notifSound= ()=>{
    //   const popSound = new Audio('yellow.mp3');
    //   popSound.play();

    // }

    const formattedTime= (time: number)=>{
      const min= Math.floor(time/60)
      const sec= time% 60

      return `${String(min).padStart(2,'0')} : ${String(sec).padStart(2,'0')}`
    }

    return {time, startTime, formattedTime}

  }
});
</script>

<style>
body{
  
  text-align: center;
  position: absolute;
  align-items: center;
  justify-content: center;
  top: 40%;
  left: 50%;
  transform: translate(-50%, -50%);
}
.container{ 
  margin: 0 auto;
  position: relative;
  width: 400px;
  height: 400px;
  border-radius: 50%;
  border: 4px solid #717171;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  background-color: #FF6347;
  font-size: 30px;
  font-family: Helvetica;
 
}

</style>
