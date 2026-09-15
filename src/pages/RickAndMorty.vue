<script setup>
import axios from "axios";
import { ref, watch } from "vue";

import CharacterCard from "../components/CharacterCard.vue";
import PaginationBar from "../components/PaginationBar.vue";

let characters = ref([]);
let currentPage = ref(1);
let totalPages = ref(0);

let characterList = ref(null);

async function getCharacters(page) {
    const res = await axios.get(
        `https://rickandmortyapi.com/api/character?page=${page}`
    );

    characters.value = res.data.results;
    totalPages.value = res.data.info.pages;
}

watch(
    currentPage,
    async (page) => {
        await getCharacters(page);

        characterList.value?.scrollIntoView({
            behavior: "smooth",
            block: "start",
        });
    },
    { immediate: true }
);
</script>

<template>
    <div ref="characterList">
        <div class="columns is-multiline">
            <div class="column is-3" v-for="character in characters" :key="character.id">
                <CharacterCard :character="character"></CharacterCard>
            </div>
        </div>

        <PaginationBar :current-page="currentPage" :total-pages="totalPages" @page-change="currentPage = $event">
        </PaginationBar>
    </div>
</template>