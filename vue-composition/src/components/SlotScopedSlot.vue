<template>
    <div>
        <slot :text="message"></slot>
        <slot :text="message1"></slot>
    </div>
</template>
<script setup>
   const message = "This is from child prop1 componenet";
   const message1 = "This is from child prop2 componenet";
</script>