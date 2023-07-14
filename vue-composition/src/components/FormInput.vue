<template>
  <div>
    <div>Form input Binding</div>
    <input :value="text" @input="$event => text = $event.target.value"><span>{{ text }}</span>
    <input v-model="text" ><span>{{ text }}</span>
    <input type="checkbox" v-model="checked">{{ checked }}
    <div>Group Check box</div>
    <input type="checkbox" value="today1" v-model="isChecked">
    <input type="checkbox" value="today2" v-model="isChecked">
    <input type="checkbox" value="today3" v-model="isChecked">
    <span>Multi Check : {{ isChecked }}</span>
  <div>Radio Element</div>
     <input type="radio" value="male" v-model="isSelected">Male | 
     <input type="radio"  value="female" v-model="isSelected">Female
     <div>Selection</div>
     <div>Slected Item : {{ selectedItem }}</div>
     <select v-model="selectedItem">
        <option disabled>Select a item</option>
        <option>A</option>
        <option>B</option>
        <option>C</option>
     </select>
     <div>Dynamic select : {{ selectDItem }}</div>
     <select v-model="selectDItem">
        <option v-for="option of options" :key=" option.value" :value="option.text">{{ option.text }}</option> 
     </select>
     <br>
     <input v-model.lazy="msg1" />{{ msg1 }}<br>
     <input v-model.trim="msg2" />{{ msg2}}<br>
     <input v-model.number="msg3" />{{ msg3 }}<br>
  </div>
</template>

<script setup lang="ts">
import { ref } from "vue";

let text = ref("my Test");
let checked = ref(true);
let isChecked = ref([]);
let isSelected = ref("");
let selectedItem = ref("");
let selectDItem = ref("");
let msg1 = ref("");
let msg2 = ref("");
let msg3 = ref("");

let options =ref([
    {text:"A",value:"A"},
    {text:"B",value:"B"},
    {text:"C",value:"C"}
    ])
</script>

<style>

</style>