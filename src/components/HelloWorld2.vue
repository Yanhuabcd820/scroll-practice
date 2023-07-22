<script setup>
import { watch,computed, ref } from 'vue'
import { useWindowScroll } from '@vueuse/core'
const { y } = useWindowScroll()
const imgLength = 13799
const imgFrame = 19
const imgHeight = 719 
const positionCal = ref(0)
const windowHeight = window.innerHeight
watch(y,()=>{
  console.log(y.value)
  positionCal.value = (imgLength / 8000) * (y.value)
  console.log(imgHeight)
  console.log('MATH',Math.floor(positionCal.value / imgHeight)*imgHeight)
  if(y.value >= 7000){
    window.scrollTo( 0, 0 );
  }
  
})
const positionGo = computed(()=>{
  return (Math.floor(positionCal.value / imgHeight)*imgHeight+35)*-1
})
</script>

<template>
  <div class="wrap">
  <div class="sprite" :style="`background-position:0 ${positionGo}px`"></div>
  <div class="bg">
    <img src="../assets/images/bg.jpg" alt="">
  </div>
  // wewqeqweqwewqeqweqwewqeqweqwewqeqweqwewqeqweqwewqeqweqwewqeqweq
  // <br>
  // wewqeqweqwewqeqweqwewqeqweqwewqeqweq
  // <br>
  // wewqeqweqwewqeqweqwewqeqweqwewqeqweqwewqeqweqwewqeqweqwewqeqweq
  // <br>
  // wewqeqwe
  // wewqeqweqwewqeqweqwewqeqweqwewqeqweqwewqeqweqwewqeqweqwewqeqweq
  // <br>
  // wewqeqwe
  // wewqeqweqwewqeqweqwewqeqweqwewqeqweqwewqeqweqwewqeqweqwewqeqweq
  // <br>
  // wewqeqwe
  </div>
</template>

<style scoped>
.wrap{
  height: 8000px;
  width: 100%;
  border: 2px solid #f00;
}
.sprite {
  position: sticky;
  top: 50px;
	width:796px;
  height:719px;
  display:block;	
  background:transparent url('../assets/images/robot.png') no-repeat;	
  /* background:transparent url('images/spritesheet-jump.png') 0 0 no-repeat;	 */
  /*// animation: walker 1s steps(19) infinite;*/
  border: 1px solid;
}

/*
// @keyframes walker {
//   from {background-position:0 -100px;}
//   to {background-position:0 -13799px;}
// }*/
</style>
