<template>
    <div>
        <h2>THis is from First Component</h2>
        <h3>{{ props.message }}</h3>
        <button>CLick me</button>
        <button @click="changeMessage">CHange message</button>
    </div>
</template>

<script setup>
const props =defineProps(['message'])


const changeMessage = ()=>{
    // message from chilld component
}

</script>

<style scoped>
h2,h3,h1{
    color:red;
}
</style>