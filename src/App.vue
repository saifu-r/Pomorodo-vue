<template>
  <div class="app">
    <div class="title">
      <div class="the"><h4>THE</h4></div>
      <h2>P<img src="../icons/tomato.png" alt="tomato">MODORO APPLICATION</h2>
      
    </div>
    <h3 style="font-family: Helvetica;">Press to begin</h3>
    <div class="container">
      <h5 v-if="isTime1===true" style="color: green;">WORK</h5>
      <h5 v-else style="color: blue;">BREAK</h5>
      <h1 v-if="isTime1===true" >{{ formattedTime(time1) }}</h1>
      <h1 v-else>{{ formattedTime(time2) }}</h1>
      <h3 @click="startTime" v-if="state==='stopped'"><img src="../icons/start.png" alt="start" ></h3>
      <h3 @click="stopTime" v-else-if="state==='running' && isTime1===true"><img src="../icons/stop.png" alt="stop"></h3>
      <h3 @click="startTime" v-else-if="state==='paused'"><img src="../icons/resume.png" alt=""></h3>
    </div>
    <br>
    <img v-for="index in cycleCount" :key="index" src="../icons/check.png" alt="check">
  
    
  </div>

</template>
<script lang="ts">
import { defineComponent, ref } from 'vue';



export default defineComponent({
  name: 'App',
  components: {},
  setup(){
    const time1 = ref(1500);
    const isTime1 = ref(true);
    const isTime2 = ref(false);
    const time2 = ref(300);
    const interval1 = ref<number | undefined>(undefined);
    const interval2 = ref<number | undefined>(undefined);
    let cycleCount = ref(0);

    const state= ref<'stopped'| 'paused'| 'running'>('stopped')

    const deduceTime1 = () => {
      if (time1.value > 0) {
        time1.value--;
      } else if (time1.value === 0) {
        clearInterval(interval1.value);
        isTime1.value = false;
        isTime2.value = true;
        time2.value = 300; // Reset time for the break
        interval2.value = setInterval(deduceTime2, 10);
      }
    };

    const deduceTime2 = () => {
      if (time2.value > 0) {
        time2.value--;
      } else if (time2.value === 0) {
        clearInterval(interval2.value);
        isTime1.value = true;
        isTime2.value = false;
        cycleCount.value++;

        if (cycleCount.value < 4) {
          // Start the next cycle
          time1.value = 1500; // Reset time for the work
          interval1.value = setInterval(deduceTime1, 10);
        } else {
          // Reset after 4 cycles
          // cycleCount.value = 0;
          time1.value = 1500; // Reset time for the work
          isTime1.value = true;
          isTime2.value = false;
        }
      }
    };

    const startTime = () => {
      // Start the first cycle
      interval1.value = setInterval(deduceTime1, 10);
      isTime1.value = true;
      isTime2.value = false;
      state.value= 'running'
    };

    const stopTime = () => {
      clearInterval(interval1.value);
      clearInterval(interval2.value);
      state.value= 'paused'
    };

    const resetTime = () => {
      stopTime();
      cycleCount.value = 0;
      time1.value = 1500; // Reset time for the work
      time2.value = 300; // Reset time for the break
      isTime1.value = true;
      isTime2.value = false;
    };

    
    
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

    return {time1,time2, startTime, formattedTime, isTime1, isTime2, cycleCount, state, stopTime}

  }
});
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=REM&display=swap');
.title{
  font-family: 'REM', sans-serif;
  font-size: 30px;
  color: #c30232;
  font: bold;
  text-align: left; /* Align text to the left */
  
}
h4, h2, h5 {
  margin: 0;
  display: block; /* Display as block elements */
}

.the{
  color: black;
  font-family: 'Borel', cursive;
  
}
img{
  width: 40px;
}

body{
  text-align: center;
  position: absolute;
  align-items: center;
  justify-content: center;
  top: 45%;
  left: 50%;
  transform: translate(-50%, -50%);
  background: #a1a1a1;
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
  background-color: #e6d5d2;
  font-size: 30px;
  font-family: Helvetica;
 
}

</style>
