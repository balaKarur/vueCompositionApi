<template>
    <div>
        <hr>
        <div>Title : {{postItem.Title}}</div>
        <div>Id : {{ postItem.Id }}</div>
        <div>
            <button @click="$event => $emit('editPost',postItem.Id)">Template Emit - Edit Title</button>
            <button @click="updateTitle(postItem.Id)">API - Edit Title</button>
            </div>
    </div>
</template>
<script setup>
defineProps({
    postItem:{
        type:Object,
        required:true
    }
})
//defineEmits mean macro , its global
//let emits = defineEmits(["editPost"]);// need to place out side function 
let emits = defineEmits({
    editPost(id){
        if(id && typeof id === 'number')
        {
            return true;
        }
        return false;
    }
})
function updateTitle(id){
    emits("editPost",id);
}

</script>