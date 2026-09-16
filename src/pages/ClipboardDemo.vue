<script setup>
import { ref } from "vue";

const text = ref("Hello from Clipboard API!");
const result = ref("");
const error = ref("");

async function copyText() {
    result.value = "";
    error.value = "";

    if (!navigator.clipboard) {
        error.value = "Clipboard API is not supported in this browser.";
        return;
    }

    try {
        await navigator.clipboard.writeText(text.value);
        result.value = "Text copied to clipboard!";
    } catch (err) {
        error.value = "Could not copy text.";
    }
}

async function readClipboard() {
    result.value = "";
    error.value = "";

    if (!navigator.clipboard) {
        error.value = "Clipboard API is not supported in this browser.";
        return;
    }

    try {
        const clipboardText = await navigator.clipboard.readText();
        result.value = `Clipboard contains: ${clipboardText}`;
    } catch (err) {
        error.value = "Could not read clipboard. Permission may be denied.";
    }
}
</script>

<template>
    <div class="content">
        <h1>Clipboard API Demo</h1>

        <p>
            This demo can copy text to the clipboard and read text from it.
        </p>

        <div class="field">
            <label class="label">Text to copy</label>

            <div class="control">
                <input v-model="text" class="input" type="text" />
            </div>
        </div>

        <div class="buttons">
            <button class="button is-primary" @click="copyText">
                Copy Text
            </button>

            <button class="button is-info" @click="readClipboard">
                Read Clipboard
            </button>
        </div>

        <div v-if="result" class="notification is-success">
            {{ result }}
        </div>

        <div v-if="error" class="notification is-danger">
            {{ error }}
        </div>
    </div>
</template>