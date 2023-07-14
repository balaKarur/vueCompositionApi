<template>
  <div>
    <input id="counter1" :ref="(el) => counterApiRef(el)" value="test"> 
    <h1>8){{ title }}</h1>
  </div>
  <div>Using Ref</div>
  <div class="text-center">
    <h2>{{ componentName }}</h2>
  </div>
  Update Name : <input type="text" v-model="componentName" />
  <button @click="increment()">+</button>
  <span>{{ counter }}</span>
  <span>{{ counterData.counter }}</span>

  <button @click="decreament()">-</button>
  <br />

  <hr />
  <div>Using reactive</div>
  <div class="text-center">
    <h2>{{ counterData.conponentName }}</h2>
  </div>
  Update Name : <input type="text" v-model="counterData.conponentName" /><br />
  <button @click="incrementObj()">+</button>

  <span>{{ counterData.counter }}</span>

  <button @click="decreamentObj()">-</button>
  <div>The counter vlaue is Odd or even = {{ oddOrEven }}</div>
  Testing 2 way binding normal way<input type="text" v-model="normalData" />
  <label>{{ normalData }}</label>
  <div>Ref with v-for</div>
  <div v-for="item in items" :key="item" ref="itemRef">{{item}}</div>
</template>
<script setup>
import {
  computed,
  reactive,
  ref,
  onBeforeMount,
  onMounted,
  onBeforeUpdate,
  onUpdated,
  onBeforeUnmount,
  onUnmounted
} from 'vue'
let items = ref([1,2,3,4]);
let itemRef = ref([]);//thsi will fill with dom object 
console.log("Array of itemRef dom element : "+itemRef);
let title = 'Counter Example'
//let normalData = "normalData";
let normalData = ref('normalData')
let counter = ref(0)
let componentName = ref(' Counter component')
const counterApiRef = function (){
    console.log("--->counterApiRef");
}
let counterData = reactive({
  counter: 0,
  conponentName: 'Counter component'
})
const oddOrEven = computed(() => {
  return counterData.counter % 2 == 0 ? 'Even' : 'Odd'
})

/*function increment(){
    counter.value++
}*/
const increment = () => {
  counter.value++
}
function decreament() {
  counter.value--
}
const incrementObj = () => {
  counterData.counter++
}
function decreamentObj() {
  counterData.counter--
}
//life cycle hook
onBeforeMount(() => {
  console.log('Child onBeforeMount')
})
onMounted(() => {
  console.log(' Child onMounted');
  console.log("Array of itemRef dom element : "+itemRef.value);
})
onBeforeUpdate(() => {
  console.log('Child onBeforeUpdate')
})
onUpdated(() => {
  console.log('Child onUpdated')
})
onBeforeUnmount(() => {
  console.log('Child onBeforeUnmount')
})
onUnmounted(() => {
  console.log('Child onUnmounted')
})
defineExpose({
    increment
})

</script>
