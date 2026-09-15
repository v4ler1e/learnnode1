<script setup>
import { computed } from "vue";

const props = defineProps({
    currentPage: {
        type: Number,
        required: true,
    },
    totalPages: {
        type: Number,
        required: true,
    },
});

const emit = defineEmits(["page-change"]);

const pages = computed(() => {
    const total = props.totalPages;
    const current = props.currentPage;

    if (total <= 7) {
        return Array.from({ length: total }, (_, i) => i + 1);
    }

    if (current <= 4) {
        return [1, 2, 3, 4, 5, "...", total];
    }

    if (current >= total - 3) {
        return [
            1,
            "...",
            total - 4,
            total - 3,
            total - 2,
            total - 1,
            total,
        ];
    }

    return [
        1,
        "...",
        current - 1,
        current,
        current + 1,
        "...",
        total,
    ];
});

function changePage(page) {
    if (
        typeof page === "number" &&
        page >= 1 &&
        page <= props.totalPages &&
        page !== props.currentPage
    ) {
        emit("page-change", page);
    }
}
</script>

<template>
    <nav class="pagination is-centered my-4">
        <button class="pagination-previous" :disabled="currentPage === 1" @click="changePage(currentPage - 1)">
            Previous
        </button>

        <button class="pagination-next" :disabled="currentPage === totalPages" @click="changePage(currentPage + 1)">
            Next
        </button>

        <ul class="pagination-list">
            <li v-for="(page, index) in pages" :key="`${page}-${index}`">
                <span v-if="page === '...'" class="pagination-ellipsis">
                    &hellip;
                </span>

                <button v-else class="pagination-link" :class="{ 'is-current': page === currentPage }"
                    @click="changePage(page)">
                    {{ page }}
                </button>
            </li>
        </ul>
    </nav>
</template>