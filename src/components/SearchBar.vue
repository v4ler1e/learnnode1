<script setup>
//what I get

//character?page=1
//character?page=1&name=m
//character?page=1&name=mo
//character?page=1&name=mor
//character?page=1&name=mort

// Questions:
// 1. How many API requests were made while typing "morty"?
// 5 requests, one for each typed character.
//
// 2. What happens if a slow request from keystroke 2 arrives after keystroke 5?
// The older request can overwrite the newer result,
// so the page may show outdated characters.
//
// 3. How does this affect the server and the user experience?
// It creates too many unnecessary API requests,
// increases server load, and can show incorrect or flickering results.
// This is called request flooding and a race condition.

import { ref } from "vue";

const query = ref("");

const emit = defineEmits(["search"]);

function search() {
    emit("search", query.value);
}
</script>

<template>
    <div class="field mb-4">
        <div class="control">
            <input v-model="query" class="input" type="text" placeholder="Search character..." @input="search" />
        </div>
    </div>
</template>
