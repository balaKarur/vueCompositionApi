<template>
  <div>Post Title : {{ postDetails.Title }}</div>
  <div>Name : {{ postName }}</div>
  <div>Message : {{ message }}</div>
  <div v-if="person != undefined">Person Name : {{person.name }}</div>
  <div v-if="person != undefined">Person Age : {{person.age }}</div>
  <button @click.prevent="($event)=> updateTitle()">Update Title from Parent Function</button>
</template>
<script setup>
import Person from './Person';
    // let props = defineProps<{
    //     postName:{
    //         type:String,
    //         default:"MY default post"
    //     },
    //     postDetails:{
    //         type:Object,
    //         required:true,
            
    //     }}>();
    let props = defineProps({
        postName:{
            type:String,
            default:"MY default post"
        },
        postDetails:{
            type:Object,
            //required:true
            default(rowProps){
                return {
                        Title: 'Default props parent to child',
                        Id: 42
                        }
                }
            },
            // message:{
            //     type:String,
            //     validator(value){ 
            //         return ['success','warning','']
            //     }

             message:{
                validator(value){ 
                    return ['success','warning','']
                }
            },
            updateTitle:{
                type:Function,
                default(){
                    return "Welcom"
                }
            },
            person:Person
        });
</script>
