<script setup>
import First from './components/FirstComponent.vue'
import { ref } from 'vue'

const message = ref("THis is from parent component")

const actionFromParent = ()=>{
  alert("THis is from parent component")
}
</script>

<template>
<div>
  <h1>Hello class</h1>
  <First :message="message"/>
</div>

</template>

<style>
</style>
