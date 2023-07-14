<template>
    <div>
        <header>
           <slot name="header" message="This is header"></slot>
        </header>
        <main>
            <slot name="main" message="This is main"></slot>
            <slot :text="message"></slot>
            <slot  message="This is default"></slot>
        </main>
        <footer>
            <slot name="footer" message="This is footer"></slot>
        </footer>
    </div>
</template>
<script setup>
const message="This is default message form child";
</script>