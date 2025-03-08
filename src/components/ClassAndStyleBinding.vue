<script setup lang="ts">
import { computed, reactive, ref } from 'vue';
import Pcomponent from '../module/pcomponent';

// Bind a class to an element with ref
const msgRef = ref('Message Ref');
const isActive = ref(true);
const hasError = ref(false);

// Bind a class to an element with reactive
const msgReactive = ref('Message Reactive');
const classObject = reactive({
  active: true,
  'text-danger': true,
  'animate': false
});

// Bind a class to an element with computed
const msgComputed = ref('Message Computed');
const isError = ref(true);
const type = ref({ type: 'danger' });
const classObjectComputed = computed(() => ({
    active: isActive.value,
    'text-danger': isActive.value && isError.value,
    'type': type.value.type === 'danger'
}));

// Bind a style to an element with array syntax
const msgArray = ref('Message Array');
const activeClass = ref('active');
const successClass = ref('text-success');

// Bind a style in toogled class
const msgToogled = ref('Correct');
function toogled() {
    msgToogled.value = msgToogled.value === 'Correct' ? 'Incorrect' : 'Correct';
}
const toogledClass = ref('active');

// Bind a style to component will render on latest class
/**
 * Example Component: <p class="foo bar baz boo">Hi!</p>
 * If you want to add a new class to the component, you can use the following code:
 * <MyComponent :class="{ active: isActive }" />
 * The component will render as <p class="foo bar baz boo active">Hi!</p>
 */

// Binding inline style
const fontSize = ref('20');
const objectStyle = reactive({
    color: 'red',
    fontSize: '30px'
});
const overideStyle = reactive({
    color: 'blue',
    fontSize: '40px'
})
</script>
<template>
    <h1>Class And Style Binding</h1>
    <!-- class="static active" -->
    <p class="static" :class="{active: isActive, 'text-danger': hasError}">{{ msgRef }}</p>
    <!-- class="static active text-danger" -->
    <p class="static" :class="classObject">{{ msgReactive }}</p>
    <!-- class="static active text-danger type" -->
    <p class="static" :class="classObjectComputed">{{ msgComputed }}</p>
    <!-- class="active text-success" -->
    <p :class="[activeClass, successClass]">{{ msgArray }}</p>
    <!-- Toogled class -->
    <p :class="[{[toogledClass]: msgToogled === 'Correct'}]">{{ msgToogled }}</p>
    <button @click="toogled">Toogle</button>
    <!-- Binding inline style -->
    <div :style="{ 'font-size': fontSize + 'px' }">Inline Style</div>
    <!-- Binding inline style with object syntax -->
    <div :style="objectStyle">Object Style</div>
    <!-- Binding inline style with array syntax -->
    <div :style="[fontSize, objectStyle, overideStyle]">Array Style</div>
</template>
<style scoped>
.active {
  text-decoration: underline;
}
.text-danger {
  color: red;
}
.text-success {
  color: green;
}
.type {
  font-weight: bold;
}
</style>