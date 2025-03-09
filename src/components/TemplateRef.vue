<script setup lang="ts">
/**
 * Template Ref
 * Template Ref is used to access the DOM element in the template.
 * 
 * Accessing ref
 * To obtain with composition API, we can use the useTemplateRef().
 * Ref can be access after component mounted.
 * The default value is null on first render.
 * If want to watch the changes of template ref
 * make sure to put it inside the watchEffect() which the ref has null value.
 * Example:
 * watchEffect(() => {
 *    if (ref.value) {
 *      ref.value.focus();
 *    }
 * });
 * 
 * Ref inside v-for
 * Not guaranteed the same order as the source array.
 * 
 * Function ref
 * Ref attribute can also be bound to a function.
 * Which will called on each component updated.
 * Use directive :ref="fn" to bind the function ref.
 * 
 * Ref on component
 * Ref can also use in child component
 * Component using <script setup> are private by default.
 * A parent component won't be able to access the ref of the child component.
 * Unless, the child component use defineExpose() to expose the ref.
 * Example:
 * defineExpose({ ref });
 */
import { ref, useTemplateRef, watchEffect, defineExpose, onMounted, VNodeRef } from 'vue';

const score = ref<number>(0);
const fullname = ref('');
const refFullname = useTemplateRef('fullnameRef');

onMounted(() => {
    refFullname.value?.focus();
});

watchEffect(() => {
    if (score.value > 1 && refFullname.value) {
        refFullname.value.focus();
    }
});

defineExpose({ refFullname, score });

function refInputNumber(ref: VNodeRef) {
    console.log(ref);
    return ref;
}

function increment() {
    score.value++;
}

</script>
<template>
    <div>
        <h1>Template Ref</h1>
        <input type="text" v-model="fullname" ref="fullnameRef" />
        <input type="number" v-model="score" :ref="refInputNumber" />

        <div>
            <button @click="increment">Increment</button>
        </div>
    </div>
</template>