<script setup lang="ts">
import { computed, reactive, ref } from "vue";

// v-for directive for an array
const items = reactive([
    { id: 1, name: "Item 1" },
    { id: 2, name: "Item 2" },
    { id: 3, name: "Item 3" },
    { id: 4, name: "Item 4" },
    { id: 5, name: "Item 5" },
]);

// v-for directive for an object
const person = reactive({
    name: "John Doe",
    age: 25,
});

// v-for directive for an range
const range = ref(10);

// v-for directive for template with v-if
const todos = ref([
    { id: 1, text: "Learn Vue 3", done: true },
    { id: 2, text: "Learn React", done: false },
    { id: 3, text: "Learn Angular", done: false },
    { id: 4, text: "Learn Svelte", done: false },
]);

// use computed if you do not want mutating or reseting the original data
const prices = ref([1, 2, 3, 4, 5, 6, 7, 8, 9, 10]);
const evenPrices = computed(() => prices.value.filter((p) => p % 2 === 0));

// use function for computed a loops data
const sets = ref([
    [1, 2, 3, 4, 5],
    [6, 7, 8, 9, 10]
])

function even(numbers) {
    return numbers.filter((n) => n % 2 === 0);
}
</script>

<template>
    <div>
        <h1>List Rendering</h1>
        <ul>
            <li v-for="item in items" :key="item.id">
                {{ item.name }}
            </li>
        </ul>
        <ul>
            <li v-for="({ id, name }, index) in items" :key="id">
                {{ index }} - {{ id }} - {{ name }}
            </li>
        </ul>
        <ol>
            <li v-for="(value, key) in person" :key="key">
                {{ key }}: {{ value }}
            </li>
        </ol>
        <template v-for="todo in todos" :key="todo.id">
            <li v-if="todo.done">
                {{ todo.text }}
            </li>
        </template>
        <p><span v-for="n in range">{{ n }}<span v-show="n < 10">,</span></span></p>
        <ul>
            <li v-for="price in evenPrices" :key="price">
                {{ price }}
            </li>
        </ul>
        <ul>
            <li v-for="(set, index) in sets" :key="index">
                <ul>
                    <li v-for="n in even(set)" :key="n">
                        {{ n }}
                    </li>
                </ul>
            </li>
        </ul>
    </div>
</template>
