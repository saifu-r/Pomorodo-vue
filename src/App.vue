<template>
  <pomorodo-app></pomorodo-app>
</template>
<script lang="ts">
import { defineComponent, ref } from 'vue';
import PomorodoApp from './components/PomorodoApp.vue'



export default defineComponent({
  name: 'App',
  components: {PomorodoApp},
  
});
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=REM&display=swap');

.title {
  font-family: 'REM', sans-serif;
  font-size: 30px;
  color: #c30232;
  font: bold;
  text-align: left;
  /* Align text to the left */

}

h4,
h2,
h5 {
  margin: 0;
  display: block;
  /* Display as block elements */
}

.the {
  color: black;
  font-family: 'Borel', cursive;

}

img {
  width: 40px;
}

body {
  text-align: center;
  position: absolute;
  align-items: center;
  justify-content: center;
  top: 45%;
  left: 50%;
  transform: translate(-50%, -50%);
  background: #a1a1a1;
}

.container {
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

}</style>
