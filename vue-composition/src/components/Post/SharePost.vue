<template>
    <div>This is Share Post  : {{ message }}</div>
    <div>message From App Thru Inject  : {{ messageFromApp.message1 }}</div>
    <button @click="invokeUpdateMessageFromApp">Update Message form App</button>
</template>
<script setup>
import { inject } from 'vue';

defineProps({
    message:String
})
const messageFromApp = inject("MessageFromApp");
function invokeUpdateMessageFromApp(){
    messageFromApp.updateMessageFromApp("Mesage from Child");
}
</script>