<script setup>
import { ref } from 'vue';
import axios from 'axios';

let rate = ref('');

axios.get('https://api.exchangerate.host/live', {
    params: {
        access_key: '7886e7cab40defc3eb52cad09232f9f9',
        currencies: 'EUR'
    }
}).then(res => {
    rate.value = res.data.quotes.USDEUR;
});
</script>

<template>
    <div class="content">
        <h1>1 USD = {{ rate }} EUR</h1>
    </div>
</template>