<script setup>
import { computed } from "vue";

const props = defineProps({
    color: {
        type: String,
        default: "primary",
        validator(value) {
            return [
                "primary",
                "link",
                "info",
                "success",
                "warning",
                "danger",
                "dark",
            ].includes(value);
        },
    },

    size: {
        type: String,
        default: "",
        validator(value) {
            return ["", "small", "medium", "large"].includes(value);
        },
    },

    outlined: Boolean,
    rounded: Boolean,
    loading: Boolean,
    disabled: Boolean,
    light: Boolean,
    fullwidth: Boolean,
});

const classes = computed(() => ({
    [`is-${props.color}`]: true,
    [`is-${props.size}`]: props.size !== "",
    "is-outlined": props.outlined,
    "is-rounded": props.rounded,
    "is-loading": props.loading,
    "is-light": props.light,
    "is-fullwidth": props.fullwidth,
}));
</script>

<template>
    <button class="button" :class="classes" :disabled="disabled">
        <slot></slot>
    </button>
</template>