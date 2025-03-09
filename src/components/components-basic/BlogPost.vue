<script setup lang="ts">

const props = defineProps(['title']);
const emit = defineEmits(['updateFontSize', 'multipleFont']);

</script>
<template>
    <div>
        <h3>{{ props.title }}</h3>
        <button @click="$emit('updateFontSize')">Increase Font Size</button>
    </div>
</template>