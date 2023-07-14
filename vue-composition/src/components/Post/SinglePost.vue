<template>
    <div>
        <div>This is Single Post : {{ message }}</div>
        <share-post :message="message"></share-post>
    </div>
</template>
<script setup>
import SharePost from './SharePost.vue';
defineProps({
    message:String
})

</script>