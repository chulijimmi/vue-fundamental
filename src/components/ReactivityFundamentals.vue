<script setup>
import { nextTick, reactive, ref } from 'vue';
const count = ref(0);
function increment() {
    count.value++;
}
function decrement() {
    count.value--;
    console.log('decremented');
}

async function decrementUpdatingDom() {
    decrement();
    await nextTick();
    console.log('DOM updated');
}
const person = ref({ name: 'John Doe', age: 25 });
function updatePerson() {
    person.value.name = 'Jane Doe';
    person.value.age = 30;
}
const order = reactive({ items: ['Apple', 'Banana', 'Cherry'] });
function addItem() {
    const item = prompt('Enter an item to add');
    order.items.push(item);
}
function popItem() {
    order.items.pop();
}

// As reactive object property
const price = ref(1000);
const updatePrice = reactive({price: price.value});
console.log('updatePrice:', updatePrice.price);
console.log('price:', updatePrice.price);
updatePrice.price = 2000;
console.log('price:', updatePrice.price);
const newPrice = ref(3000);
updatePrice.price = newPrice;
console.log('price:', updatePrice.price);
console.log('price:', price.value);

// Caveat when unwrapping in templates
const jump = ref(0);
console.log(jump); // { value: 0 }
const colJump = { id: ref(0) };
console.log(colJump.id + 1); // '[object Object]1'
const { id } = colJump;
console.log(id + 1); // '[object Object]1'
console.log(id.value + 1); // 1

/**
 * Conclusion:
 * Use ref when want to use primitive types such as string, number, boolean.
 * Use ref when replacing entire object.
 * Use ref when want to declaring reactive state.
 * Use reactive when want to use object with multiple properties without replacing entire object.
 * Use reactive when want to use object with multiple properties without declaring reactive state.
 */
</script>
<template>
  <div>
    <h1>ReactiveDoc</h1>
    <p>Count is: {{ count }}</p>
    <button @click="increment">Increment</button>
    <button @click="decrement">Decrement</button>
    <button @click="decrementUpdatingDom">Decrement Updating DOM</button>
    <p>Person: {{ person }}</p>
    <button @click="updatePerson">Update Person</button>
    <li v-for="item in order.items" :key="item">{{ item }}</li>
    <button @click="addItem">Add Item</button>
    <button @click="popItem">Pop Item</button>
    <p>Price: {{ price }}</p>
    <p>Update Price: {{ updatePrice.price }}</p>
    <p>Id: {{ id + 1 }}</p>
  </div>
</template>