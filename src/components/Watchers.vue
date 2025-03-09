<script setup lang="ts">
/**
 * Watchers
 * Should be used syncronous operations rather than asyncronous operations.
 * Watchers are used to watch the changes in the data and perform some operations.
 * Watch Source Types for several cases where watchers are useful:
 * 1. Use watch directly on single ref or reactive.
 * 2. Use watch source from computed ref or reactive object.
 * 3. Use watch with getter and setter.
 * 4. Use watch for an array of refs or reactives on multiple source.
 * 
 * Deep watcher
 * Perform deep watcher on the object or array to watch the changes in the nested properties.
 * Use the option { deep: true } to watch the changes in the nested properties.
 * 
 * Eager watcher
 * Watch is lazy by default, it will not run the first time when the component is mounted.
 * To make it eager, use the option { immediate: true }.
 * 
 * Once watcher
 * watch will run the first time when the component is mounted.
 * If want callback to trigger only once, use the option { once: true }.
 * In v 3.5 can be simplified by using watchEffect.
 * WatchEffect is a combination of watch and watch source.
 * 
 * Side effect cleanup
 * To cancel perform side effect on asyncronous request such as call API when the state changes.
 * Only available in v 3.5
 * use onWatcherCleanup() inside of watcher is called when the watcher is stopped.
 * or, use onCleanup() inside of watcher to cleanup all the watchers.
 * 
 * Callback flush timing
 * By default, the watcher callback is called after parent component updated.
 * And, before the owner component's DOM is updated.
 * To access the owner component's DOM in watcher callback after Vue has updated it.
 * This can be use in watch or watchEffect.
 * Use the option { flush: 'post' }.
 * Post-flush watchEffect also has a convenience alias, watchPostEffect.
 * 
 * Sync watcher
 * It is also possible to create a watcher that fire synchronously, before any Vue managed DOM updates.
 * This can be use in watch or watchEffect.
 * To make it syncronous, use the option { flush: 'sync' }.
 * Sync watchEffect also has a convenience alias, watchSyncEffect.
 * 
 * Stop watcher
 * The key is the watcher must be create syncronously.
 * To manually stop the watcher, use returned handle function.
 * This works for both watch and watchEffect/
 * By declaring variables to store the watcher, it can be stopped manually.
 * Example:
 * const stop = watch(() => state.value, () => {});
 * stop();
 * Do not use async function inside of watcher.
 * Instead, change the logic to predict the state change, then watcher will stop automatically.
 * Example:
 * const data = ref(null);
 * watchEffect(() => {
 *    if (data.value) {
 *       // do something
 *    }
 * });
 */
</script>
<template>
    <div>
        <h1>Watchers</h1>
    </div>
</template>