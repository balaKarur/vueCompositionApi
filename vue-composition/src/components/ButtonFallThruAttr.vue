<template>
    <div>{{$attrs}}</div>
    <Button  class="child" style="color:red" @click="childClick($event)" v-bind="$attrs">My Btn</Button>
</template>
<script setup >
import { onUpdated, useAttrs } from 'vue';

defineOptions({
  inheritAttrs: false
})
const attrs = useAttrs();

function childClick(e){
    console.log("child Click ...");
     console.log(e.target);
     attrs.style.color="blue";
}

onUpdated(() => {
  console.log("onUpdated event triggered....");
})
</script>
<style>
   .child{
     font-size: 20px;
   }
</style>