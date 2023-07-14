<template>
<!-- $attrs.class inherite class names from parent div -->
    <h3 :class="$attrs.class">Class Binding</h3>
    <div :class="{active:isActive,errorCls:isError}"> Apply class Dynamically1</div>
    <div :class="[{active:isActive,errorCls:isError}]"> Apply class Dynamically2</div>
     <div :class="[isError == true ? 'errorCls' : '']"> Apply class Dynamically 4</div>
      <div :class="[{[activeClass]:isActive,errClass}]"> Apply class Dynamically name</div>
    <!-- <div :class="classObject"> Apply class Dynamically</div> -->
    <div :class="classComputedProp"> Apply class Dynamically3</div>
    <input type="checkbox" name="" id="" >isActive
    <button v-on:click.prevent="()=>counter++">Click Me</button>
    <button v-on:click.once="()=>counter++">Can Click Me Once</button>
     <button key="()=>counter++">Can Click Me Once</button>
    <span>{{counter}}</span>
</template>
<script setup>
import { computed, reactive, ref } from "vue";
let counter = ref(0);
const isActive = ref(true);
const isError = ref(true);
const activeClass  = ref("active");
const errClass  = ref("error");
const  classObject = reactive({
    active:isActive.value,
    'errorCls':isError.value
})
const classComputedProp = computed(() => {
   return {
        active1: isActive.value && !isError.value,
        errorCls1: isError.value
   } 
})

</script>