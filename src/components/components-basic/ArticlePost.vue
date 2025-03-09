<script setup lang="ts">
interface PropsType {
    title: String,
    content: String,
}
const props = defineProps<PropsType>();
</script>
<template>
    <div>
        <p>{{ props.title }}</p>
        <p>{{ props.content }}</p>
    </div>
</template>