<script setup lang="ts">
import { reactive, ref } from 'vue';

/**
 * Conditional Rendering has several ways to render content based on conditions.
 * The options include v-if, v-else-if, v-else, and v-show.
 */

// v-if
const show = ref(true);
let isUserOnline = ref(true);
function toogleUserOnline() {
    isUserOnline.value = !isUserOnline.value;
}

console.log(isUserOnline.value)
</script>
<template>
    <h1>Conditional Rendering</h1>
    <p v-if="show">This is visible</p>
    <p v-else>This is not visible</p>
    <button @click="show = !show">Toggle</button>
    <p>User online {{ isUserOnline }}</p>
    <p v-show="isUserOnline">On Boarding</p>
    <button @click="toogleUserOnline">Toggle User Online</button>
</template>