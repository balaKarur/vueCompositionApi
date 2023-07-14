<template>
  <div>v-html</div>
  <div v-html="message"></div>
  <hr>
  <div> Adding Dynamic Attribute</div>
  <div v-bind:id="dynamicId">Dynamic Id</div>
  <hr>
  <div>Dynamically binding multiple attributes</div>
  <div v-bind="objOfAttrs">Data</div>
   <hr>
   <div>Dynamically binding Attr and key</div>
   <div :[attrKey]="attrVal"> Attr</div>
   <div>Adding Event Dynamically</div>
   <div @[eventName]="myAlert()" >Click Me and see</div>
</template>

<script setup>
const message = "<h1>Welcome All</h1>";
const dynamicId = "myId";
const objOfAttrs ={
    id : dynamicId,
    class : " my-class"
}
const attrKey = "title";
const attrVal = "This is my title";
const eventName = "click";
const eventName1 = "mouseover";
function myAlert()
{
    alert("You clicked Me...");
}
</script>

<style scoped>


</style>