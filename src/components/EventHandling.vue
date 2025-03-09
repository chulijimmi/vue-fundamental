<script setup lang="ts">
import { ref } from 'vue';

/**
 * Event handling has several topics:
 * - Listening to events, has inline handlers and method handlers.
 * - Directive v-on can be used by @ for shorthand
 * - Calling method in Inline handlers by passing arguments
 * - Accessing event in inline handlers and special $events
 * - Event modifiers
 * - Key modifiers
 * - System modifiers key
 * - Exact modifier
 * - Mouse button modifier
 */

// Listening to events inline handlers
const count = ref(0);

// Listening to events method handlers
const handleClick = () => {
    count.value++;
};

// Calling method in Inline handlers by passing arguments
function handleClickWithArgs(message: string, event: MouseEvent) {
    alert(`${message} ${event.type}`);
};

// Accessing event in inline handlers and special $events
function handleEvent(event: MouseEvent) {
    if (event.type === 'click') {
        event.preventDefault();
    }
    alert('Event type: ' + event.type);
};

// Event modifiers
function handleSubmitButton() {
    alert('Form submitted');
}

// System modifiers
function handleSystemClick() {
    const promptText = 'Control + Click me';
    alert(promptText)
}

// Exact modifier
function handleExactClick() {
    alert('Exact click');
}

// Mouse button modifier
function handleRightClick(event: MouseEvent) {
    event.preventDefault();
    alert('Right click');
}
</script>

<template>
    <!-- Listening to events inline handlers -->
    <div>
        <button v-on:click="count++">Click me {{ count }}</button>
    </div>
    <!-- Listening to events method handlers -->
    <div>
        <button @click="handleClick">Click me {{ count }}</button>
    </div>
    <!-- Calling method in Inline handlers by passing arguments -->
    <div>
        <button @click="handleClickWithArgs('Hello', $event)">Click me</button>
    </div>
    <!-- Accessing event in inline handlers and special $events -->
    <div>
        <button @click="handleEvent">Click me</button>
    </div>
    <!-- Event modifiers -->
    <div>
        <form @submit.prevent="handleSubmitButton">
            <button type="submit">Submit</button>
        </form>
    </div>
    <!-- Key modifiers -->
    <div>
        <input @keyup.enter="handleSubmitButton" placeholder="Press enter to submit" />
    </div>
    <!-- Key Alias -->
    <div>
        <input @keyup.up="count++" @keyup.down="count--" placeholder="Page down to alert" :value="count" />
    </div>
    <!-- System modifiers key -->
    <div @click.ctrl="handleSystemClick">
        Control + Click me
    </div>
    <!-- Exact modifier -->
    <div>
        <button @click.exact="handleExactClick">Click without any key</button>
    </div>
    <!-- Mouse button modifier -->
    <div @click.right="handleRightClick">
        Right click me
    </div>
</template>