<script setup lang="ts">
import { computed, reactive, ref } from 'vue';

const author = reactive({
  name: 'John Doe',
  age: 25,
  get birthYear() {
    return new Date().getFullYear() - this.age;
  },
  set birthYear(value) {
    this.age = new Date().getFullYear() - value;
  },
  books: [{ title: 'Book 1' }, { title: 'Book 2' }],
  get latestBook() {
    return this.books[this.books.length - 1];
  },
});

const publishedBooksMessage = computed(() => {
    return author.books.length > 0
        ? `Author has published ${author.books.length} books`
        : 'Author has not published any books';
});

/**
 * Compute are cache based on reactive dependencies
 * If reactive dependencies change, the computed property will re-run
 * If reactive dependencies do not change, the computed property will return the cached value
 */

// Writeable compute using getter and setter
const firstName = ref('John');
const lastName = ref('Doe');
const fullName = computed({
    get: () => `${firstName.value} ${lastName.value}`,
    set: (value) => {
        const names = value.split(' ');
        firstName.value = names[0];
        lastName.value = names[1];
    },
});
function setFullName() {
    const newFullName = prompt('Enter a new full name');
    if (newFullName) {
        fullName.value = newFullName;
    }
}

// Getting previous value
const count = ref(2);
const allwaysSmall = computed((previous) => {
    if (count.value <= 3) {
        return count.value;
    }
    return previous;
})
const currentCount = computed({
    get: (previous) =>{
        /**
         * Previous value is undefined on the first run
         * After trigger the computed property,
         * When user click updateCurrentCount button
         * It will be the previous value of the computed property
         */
        console.log('previous:', previous);
        if (count.value >= 2) {
            return count.value;
        }
        return previous
    },
    set: (newValue: number) => {
        count.value = newValue + 1;
    }
});
function updateCurrentCount() {
    currentCount.value = 4;
}

</script>
<template>
  <div>
    <h1>Computed Properties</h1>
    <p>{{ publishedBooksMessage }}</p>
    <p>{{ fullName }}</p>
    <button @click="setFullName">Set Fullname</button>
    <p>Always Small: {{ allwaysSmall }}</p>
    <p>current Count: {{ currentCount }}</p>
    <button @click="updateCurrentCount">Update Current Count</button>
  </div>
</template>