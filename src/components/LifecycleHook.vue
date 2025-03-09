<script setup lang="ts">
import { onBeforeMount, onBeforeUpdate, onMounted, onUnmounted, onUpdated, ref, useTemplateRef } from 'vue';

const msg = ref('Hello Vue 3');
const phone = ref(0);
const btnRef = useTemplateRef('btn');
const inputRef = useTemplateRef('input');

function changeMsg() {
    msg.value = 'Hello Vue 3 + TypeScript + Vite';
}

// Lifecycle Hooks in Vue 3

onBeforeUpdate(() => {
    console.log('BeforeUpdate');
});

onBeforeMount(() => {
    console.log('BeforeMount');
});

onMounted(() => {
    console.log('Mounted');
});

onUpdated(() => {
    console.log('Updated');
    inputRef.value?.focus();
});

onUnmounted(() => {
    console.log('Unmounted');
});

function handleUnmount() {
    btnRef.value?.remove();
};
</script>
<template>
    <div>
        <h1>LifecycleHook</h1>
        <div>
            <input type="text" v-model="msg" />
        </div>
        <div>
            <button ref="btn" @click="changeMsg">Change Message</button>
        </div>
        <div>
            <input type="number" ref="input" v-model="phone" />
        </div>
        <div>
            <button @click="handleUnmount">Unmount Component</button>
        </div>
    </div>
</template>