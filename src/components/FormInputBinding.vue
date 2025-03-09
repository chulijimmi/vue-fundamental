<script setup lang="ts">
import { reactive, ref } from 'vue';

/**
 * Manually wire up value binding and change event listener can use @input="modelValue = $event.target.value"
 * But it's better to use v-model directive to bind value and listen to input event, it is more simple.
 * Basic ussage of v-model directive:
 * - v-model="modelValue"
 * Value binding can use in several HTML component including:
 * - input
 * - textarea
 * - select
 * - checkbox
 * - radio
 * - select options with object value
 * Input as modifier
 */
// Basic v-model
const selected = ref('');
function showSelected() {
    alert(selected.value);
}

// Value binding input
const fullname = ref<string>('');

// Value binding textarea
const description = ref<string>('');

// Value binding select
const framework = reactive({
    selected: '',
    options: [
        { value: 'vue', label: 'Vue' },
        { value: 'react', label: 'React' },
        { value: 'angular', label: 'Angular' },
    ],
});
// Value binding checkbox
const checkbox = ref(false);
const checkboxFirst = ref(false);
const checkboxSecond = ref(false);

// Value binding radio
const radio = ref('');
const radioYesOrNo = ref('');
const radioFirst = ref('');
const radioSecond = ref('');

// Value binding select options with object value
const movies = reactive({
    selected: '',
    options: [
        { id: 1, value: 'horror', label: 'Horror' },
        { id: 2, value: 'comedy', label: 'Comedy' },
        { id: 3, value: 'drama', label: 'Drama' },
    ],
});

// Input as modifier lazy
const inputLazy = ref('');
// Input as modifier number
const inputNumber = ref(0);
// Input as modifier trim
const inputTrim = ref('');
</script>

<template>
    <!-- Basic v-model -->
    <div>
        <select v-model="selected">
            <option value="" disabled>Select</option>
            <option value="Horor">Horor</option>
            <option value="Action">Action</option>
            <option value="Comedy">Comedy</option>
        </select>
        <button @click="showSelected">Show selected</button>
    </div>
    <!-- Value binding input -->
    <div>
        <p>{{ fullname }}</p>
        <label for="fullname">Fullname: </label>
        <input type="text" v-model="fullname" placeholder="Fullname">
    </div>
    <!-- Value binding textarea -->
    <div>
        <textarea v-model="description" placeholder="Description"></textarea>
        <p>{{ description }}</p>
    </div>
    <!-- Value binding select -->
    <div>
        <select v-model="framework.selected">
            <option value="" disabled>Select</option>
            <option v-for="option in framework.options" :key="option.value" :value="option.value">{{ option.label }}
            </option>
        </select>
        <p>{{ framework.selected }}</p>
    </div>
    <!-- Value binding checkbox -->
    <div>
        <input type="checkbox" v-model="checkbox" true-value="yes" false-value="no">
        <label for="checkbox">Checkbox</label>
        <p>{{ checkbox }}</p>
        <input type="checkbox" id="first" v-model="checkboxFirst">
        <label for="first">First</label>
        <input type="checkbox" id="second" v-model="checkboxSecond">
        <label for="second">Second</label>
        <p>{{ checkboxFirst }} {{ checkboxSecond }}</p>
    </div>
    <!-- Value binding radio -->
    <div>
        <input type="radio" id="vue" value="vue" v-model="radio">
        <label for="vue">Vue</label>
        <input type="radio" id="react" value="react" v-model="radio">
        <label for="react">React</label>
        <input type="radio" id="angular" value="angular" v-model="radio">
        <label for="angular">Angular</label>
        <p>{{ radio }}</p>
        <input type="radio" id="yes" value="yes" v-model="radioYesOrNo">
        <label for="yes">Yes</label>
        <input type="radio" id="no" value="no" v-model="radioYesOrNo">
        <label for="no">No</label>
        <p>{{ radioYesOrNo }}</p>
        <input type="radio" id="first" value="first" v-model="radioFirst">
        <label for="first">First</label>
        <input type="radio" id="second" value="second" v-model="radioSecond">
        <label for="second">Second</label>
        <p>{{ radioFirst }}</p>
        <p>{{ radioSecond }}</p>
    </div>
    <!-- Value binding select options with object value -->
    <div>
        <select v-model="movies.selected">
            <option value="" disabled>Select</option>
            <option v-for="movie in movies.options" :key="movie.id" :value="{ id: movie.id }">{{ movie.label }}
            </option>
        </select>
        <p>{{ movies.selected }}</p>
    </div>
    <!-- Input as modifier lazy -->
    <div>
        <label for="inputLazy">Async Name: </label>
        <input type="text" v-model.lazy="inputLazy" placeholder="Input lazy">
        <p>{{ inputLazy }}</p>
    </div>
    <!-- Input as modifier number -->
    <div>
        <label for="inputNumber">Age: </label>
        <input type="number" v-model.number="inputNumber" placeholder="Input number">
        <p>{{ inputNumber }}</p>
    </div>
    <!-- Input as modifier trim -->
    <div>
        <label for="inputTrim">Message: </label>
        <input type="text" v-model.trim="inputTrim" placeholder="Input trim">
        <p>{{ inputTrim }}</p>
    </div>
</template>