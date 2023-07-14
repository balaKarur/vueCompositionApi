<template>
    <div>
      
        v- Model : <input type="text" :value="modelValue" @input="$event => $emit('update:modelValue',$event.target.value)"> 
        Dyamic v-model title : <input type="text" :value="title" @input="$event => $emit('update:title',$event.target.value)">
        Dyamic v-model name with Computed : <input type="text" v-model="value">
    </div>
</template>
<script setup>
import { computed } from "vue";
 const props = defineProps({
    modelValue:{
        type:String,
        required:false
    },
    title:{
        type:String,
        required:false
    },
    name:{
        type:String,
        required:false
    }
})
const emit = defineEmits("update:name");
var value = computed(
{
    get(){
        return props.name;
    },
    set(newValue){
       emit("update:name",newValue)
    }
})
</script>