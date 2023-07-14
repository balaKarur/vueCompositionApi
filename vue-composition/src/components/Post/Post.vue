<template>
    <div>Post : {{ message }}</div>
    <single-post :message="message"></single-post>
</template>
<script setup>
import SinglePost from "./SinglePost.vue"
defineProps({
    message:String
})
</script>