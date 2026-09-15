<script setup>
import { ref } from "vue";

const query = ref("");

const emit = defineEmits(["search"]);

function search() {
    emit("search", query.value);
}
</script>

<template>
    <form class="field has-addons mb-4" @submit.prevent="search">
        <div class="control is-expanded">
            <input v-model="query" class="input" type="text" placeholder="Search character..." />
        </div>

        <div class="control">
            <button class="button is-primary" type="submit">
                Search
            </button>
        </div>
    </form>
</template>