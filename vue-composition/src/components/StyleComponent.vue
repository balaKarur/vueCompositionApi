<template>
    <h3 :style="{color:activeColor,fontSize:[fontSize]}">Syle Component</h3>
 <h3 :style="[styleProperty,styleProperty1]">Syle Component by Obj</h3>
 <button @click="changeColor()" > Change Color</button>
 <h3 :style="styleReUseProperty">Syle Component by Reuse property</h3>
 <h3 :style="getStyle()">Syle Component by Api call</h3>
 
</template>
<script setup>
import { computed, reactive, ref } from "vue";

const activeColor = ref("red");
const isActive = ref("true");
const fontSize = ref("16px");
const styleProperty = reactive({
    color:"red",
    "font-size":"16px"
})
const styleProperty1 = reactive({
    border:"2px solid",
    width:"max-content"
})
//Computed has to be a function and return object
const styleReUseProperty = computed(() => {
    return {
     color:activeColor.value,
    "font-size":fontSize.value
    }
   
});
activeColor.value = "blue";
function getStyle(){
    const styleProperty1 = {
            border:"2px solid",
            width:"max-content"
        }
return styleProperty1;
     
}
function changeColor ()
{
    console.log("change color------");
    let activeColor1 = "";
    if(isActive.value == true )
    {
        activeColor1 = "green";
        isActive.value = false;
    }else{
        activeColor1 = "black";
        isActive.value = true;
    }
    activeColor.value = activeColor1;
}

</script>