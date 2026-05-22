<script setup>
import { ref } from 'vue';

let message = ref('Hello Vue!');


</script>

<template>
    <h1>{{ message.split('').reverse().join('') }}</h1>
    <button class="button is-primary" @click="message = 'Tello TA24B!'">Click me!</button>
    <input class="input" v-model="message">
</template>

<style>

</style>