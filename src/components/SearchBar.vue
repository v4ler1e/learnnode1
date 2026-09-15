<script setup>
import { ref, watch } from "vue";

const query = ref("");

const emit = defineEmits(["search"]);

watch(query, (newQuery) => {
    emit("search", newQuery);
});
</script>

<template>
    <div class="field mb-4">
        <div class="control">
            <input v-model="query" class="input" type="text" placeholder="Search character..." />
        </div>
    </div>
</template>