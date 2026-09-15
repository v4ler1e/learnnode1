<script setup>
import axios from "axios";
import { ref } from "vue";

import CharacterCard from "../components/CharacterCard.vue";
import PaginationBar from "../components/PaginationBar.vue";
import SearchBar from "../components/SearchBar.vue";

const characters = ref([]);
const currentPage = ref(1);
const totalPages = ref(0);
const searchQuery = ref("");
const noResults = ref(false);

const characterList = ref(null);

const API_URL = "https://rickandmortyapi.com/api/character";

async function fetchCharacters(page = currentPage.value) {
    noResults.value = false;

    const params = {
        page: page,
    };

    if (searchQuery.value) {
        params.name = searchQuery.value;
    }

    try {
        const res = await axios.get(API_URL, {
            params: params,
        });

        characters.value = res.data.results;
        totalPages.value = res.data.info.pages;
    } catch (error) {
        if (error.response?.status === 404) {
            characters.value = [];
            totalPages.value = 0;
            noResults.value = true;
        } else {
            console.error(error);
        }
    }
}

async function handleSearch(query) {
    searchQuery.value = query.trim();

    currentPage.value = 1;

    await fetchCharacters(1);
}

async function changePage(page) {
    currentPage.value = page;

    await fetchCharacters(page);

    characterList.value?.scrollIntoView({
        behavior: "smooth",
        block: "start",
    });
}

fetchCharacters(1);
</script>

<template>
    <div ref="characterList">
        <SearchBar @search="handleSearch"></SearchBar>

        <div v-if="noResults" class="notification is-warning">
            No characters found
        </div>

        <div v-else class="columns is-multiline">
            <div class="column is-3" v-for="character in characters" :key="character.id">
                <CharacterCard :character="character"></CharacterCard>
            </div>
        </div>

        <PaginationBar v-if="totalPages > 0" :current-page="currentPage" :total-pages="totalPages"
            @page-change="changePage"></PaginationBar>
    </div>
</template>