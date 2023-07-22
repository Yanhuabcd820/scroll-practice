<script setup>
import { watch,computed, ref } from 'vue'
import { useWindowScroll } from '@vueuse/core'
const { y } = useWindowScroll()
const imgLength = 8208
const imgFrame = 19
const imgHeight = 432
const positionCal = ref(0)
const windowHeight = window.innerHeight
const windowWidth = window.innerWidth
const bgWidth=3027
const bgPositionCal = ref(0)
watch(y,()=>{
  positionCal.value = (imgLength / ( 8000 - windowHeight )) * (y.value)
  if(y.value >= 8000-windowHeight){
    window.scrollTo( 0, 0 );
  }

  bgPositionCal.value = (bgWidth / (8000 - windowHeight)) * (y.value)*-1
  
})
const positionGo = computed(()=>{
  return (Math.floor(positionCal.value / imgHeight)*imgHeight+35)*-1
})
</script>

<template>
  <div class="wrap">
  <div class="sprite" :style="`background-position-y: ${positionGo}px`"></div>
  <div class="bg" :style="`left:${bgPositionCal}px`">
    <img src="../assets/images/bg.jpg" alt="">
  </div>

  </div>
</template>

<style>
.wrap{
  height: 8000px;
  width: 100%;
}
.sprite {
  position: sticky;
  left:30%;
  top: 40%;
	width:478px;
  height:432px;
  display:block;	
  background: url('../assets/images/robot.png') no-repeat;	
  background-size: cover;
}

.bg{
  position: fixed;
  top: 0;
  left: 0px;
  z-index: -1;
  height: 768px;
}
.bg::after{
  content:'';
  background: url('../assets/images/bg.jpg');	
  background-size: contain;
  height: 100%;
  width: 3026px;
  position: absolute;
  left: 100%;
  top: 0;
  background-color: aqua;
}
</style>
