<script setup lang="ts">

// Using a component from another file
import { ref } from 'vue';
import BlogPost from './components-basic/BlogPost.vue';
import ButtonCounter from './components-basic/ButtonCounter.vue';
import ArticlePost from './components-basic/ArticlePost.vue';

// Passing Props
const posts = ref([
    { title: 'Post 1' },
    { title: 'Post 2' },
    { title: 'Post 3' },
]);

// Listening to event
const postFontSize = ref(1);
</script>
<template>
    <div>
        <h1>Components Basic</h1>
        <p>Render Button Component</p>
        <ButtonCounter />
        <ArticlePost title="Hello vue 3" content="Lorem ipsum dolor sir amet" />
    </div>
    <div :style="{ fontSize: postFontSize + 'em' }">
        <h2>Posts</h2>
        <BlogPost v-for="post in posts" :title="post.title" :key="post.title" @updateFontSize="postFontSize += 0.1" />
    </div>
</template>