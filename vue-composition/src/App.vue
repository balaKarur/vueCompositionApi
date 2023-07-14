<template>
  <div>
    <HTMLTemplate></HTMLTemplate>
    <hr />
    <h2>Template Refs</h2>
    <input id="counter" ref="counterRef" value="test" />
    <!--
    <hr />
    <button @click.prevent="() => (showCounter = !showCounter)">showCounter</button>
    <button @click.prevent="increaseCountFromParent()">Increase count from Parent</button>
    <counter v-if="showCounter" ref="counterParentRef"></counter>

    <hr />
    <ComputedComponenet />
    <hr />
    <ClassComponenet class="foo foo1" />
    <hr />
    <StyleComponent />
    <hr />

    <FormInput />
    <hr /> 
    <div>Custom Input Componenet</div>
    <CustomeInput
      :model-value="text"
      @update:model-value="(newValue) => (text = newValue)"
      :validation="{ type: 'number', 'max-length': 10, 'min-length': 6, specialchar: '$' }"
    />
    <span>Data from custom directive{{ text }}</span>
    <div><CustomeInput v-model="text1" />{{ text1 }}</div>
    <hr />-->
    <div>Componenet Understanding</div>
    <singlePost :postDetails="postDetails" :post-name="postName" />
    <!-- Can pass Object to teh componenet -->
    <singlePost :message="ASs" :update-title="updateTitle" :person="person" />
    <singlePost1 v-for="post in posts" :post-item="post" :key="post.id" @edit-post="editPost"></singlePost1>
    <div>Normal Data binding </div>
    <CustomTextInput :model-value="searchText" @update:model-value="text => searchText= text"></CustomTextInput>
    <div>V-Model</div>
    <CustomTextInput v-model="searchText" ></CustomTextInput>
    <div>searchText : {{ searchText }}</div>
    <div>Multi v-model</div>
    <!--Multiple V-model in a component -->
    <!-- v-model
    v-model:firstname v-model:lastname
    v-model.no-hyphens
    custom modifier v-model:firstname.no-hyphens -->

    <CustomTextInput v-model:title="searchText" v-model:name="name"></CustomTextInput>
    <div>searchText : {{ searchText }}</div>
    <div>searchName : {{ name }}</div>
    <!--<div>FallThroughAttribute</div>
    <button-fall-thru-attr class="parent" style="color:rgb(0, 255, 89)" @click="parentClick($event)"></button-fall-thru-attr>
     -->
    <h3>Slot</h3>
    <slot-btn>MY Slot Button {{ text }}</slot-btn>
    <h3>Named Slot</h3>
    
    <slot-comp>
      <!-- If we have # default then need to place under # default -->
      <!--Either #default or without default slot  -->
    <!-- <div> Default SLot2</div> -->
      <template  #header>
      <div>
        Header
      </div>
    </template>
    <template #main>
         <div>Main</div>
    </template>
    <template #footer>
         <div>Footer</div>
    </template>
    <template #default>
      <div > Default SLot1</div>
    </template>
   
    </slot-comp>
    <h3>ScopedSlot</h3>
    <slot-scoped-slot v-slot="childProps">
      <div > ScopedSlot : child props -> {{ childProps }}</div>
    </slot-scoped-slot>

    <h3>SlotNamedSlotWithScopedSlot</h3>
    <slot-named-slot-with-scoped-slot  >
      <template #header="message">
             <div>This content from Child {{message}}</div>
      </template>
      <template #main="message">
        <div>This content from Child {{message}}</div>
        
      </template>
      <template #footer="message">
        <div>This content from Child {{message}}</div>
      </template>
      <template #default="message">
        <div>This content from Child {{message}}</div>
      </template>
     
    </slot-named-slot-with-scoped-slot>
    <h3>Provide and inject and Show Post Component Async</h3>
    <button @click="showpost = !showpost ">Load Post Componenet Async</button> 
    <post v-if="showpost" :message="message"></post>
  </div>
 
</template>


<script setup>
import HTMLTemplate from './components/HTMLTemplate.vue'
import counter from './components/Counter.vue'
import ComputedComponenet from './components/ComputedComponenet.vue'
import ClassComponenet from './components/ClassComponenet.vue'
import StyleComponent from './components/StyleComponent.vue'
import FormInput from './components/FormInput.vue'
import CustomeInput from './components/CustomeInput.vue'
import singlePost from './components/singlePost.vue'
import singlePost1 from './components/SinglePost1.vue'
import CustomTextInput from './components/CustomTextInput.vue'
import ButtonFallThruAttr from './components/ButtonFallThruAttr.vue';
import SlotBtn from './components/SlotBtn.vue';
import SlotComp from './components/SlotComp.vue';
import SlotScopedSlot from "./components/SlotScopedSlot.vue"
import SlotNamedSlotWithScopedSlot from "./components/SlotNamedSlotWithScopedSlot.vue";
//import post from './components/Post/post.vue';//This is sync way of loading
import LoadingComponent from './components/LoadingComponent.vue';
import Person from './components/Person'
import {
  ref,
  onBeforeMount,
  onMounted,
  onBeforeUpdate,
  onUpdated,
  onBeforeUnmount,
  onUnmounted,
  provide,
  defineAsyncComponent
} from 'vue';
//defineAsyncComponent 
//const post = defineAsyncComponent(() => import('./components/Post/post.vue'));//Deafult way of 
const post = defineAsyncComponent({
   loader: () =>{
    return new Promise((resolve,reject) => {
      setTimeout(() => {
        resolve(import('./components/Post/post.vue'));
      },1000)
    })
   },
   loadingComponent:LoadingComponent
})
const showpost = ref(false);
let text = ref('test')
let text1 = ref('text1')
let showCounter = ref(true)
let counterRef = ref(null);
let searchText = ref("");
let counterParentRef = ref(null);
let name = ref("");
let message = ref("Message from App");
let message1 = ref("Message from App");
function updateMessageFromApp(data){
  message1.value = ref(data);
}
provide("MessageFromApp",{message1,updateMessageFromApp});
let person = new Person('Bala', 20)
console.log(person.name + '  ' + person.age)
const postDetails = ref({
  Title: 'props parent to child',
  Id: 42
})
function parentClick ()
{
  console.log("parentClick ...");
  console.log(e.target);
}
const posts = ref([
  {
    Title: 'Post1',
    Id: 1
  },
  {
    Title: 'Post2',
    Id: 2
  },
  {
    Title: 'Post3',
    Id: 3
  }
])
function editPost (id){
  // let postIndex = posts.value.findIndex(post => post.Id == id);
  // let post = posts.value[postIndex];
  // post.Title = "Edited Post"
  posts.value.map(post => {
    if(post.Id == id ){
      post.Title = "Edited Post";
    }
     return post;
  }) 
}
const updateTitle = () => {
  postDetails.value.Title = 'changed from parent'
}
const postName = 'My post1'
//life cycle hook
onBeforeMount(() => {
  console.log('Parent onBeforeMount')
  console.log('counterRef' + counterRef)
})
onMounted(() => {
  console.log(' Parent onMounted')
  console.log('counterRef  ->' + counterRef.value.value)
  console.log('counterParentRef to access child ----  ->' + counterParentRef.value)
})
const increaseCountFromParent = () => {
  counterParentRef.value.increment()
}
onBeforeUpdate(() => {
  console.log('Parent onBeforeUpdate')
})
onUpdated(() => {
  console.log('Parent onUpdated')
})
onBeforeUnmount(() => {
  console.log('Parent onBeforeUnmount')
})
onUnmounted(() => {
  console.log('Parent onUnmounted')
})
const counterParentRef1 = () => {
  console.log('counterParentRef')
}
</script>
