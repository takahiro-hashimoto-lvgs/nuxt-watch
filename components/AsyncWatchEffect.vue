<script setup lang="ts">
const count = ref(0);
watchEffect(async () => {
  await new Promise((resolve) => setTimeout(resolve, 1000));
  console.log('AsyncWatchEffect', 'count', count.value);
});
const onClick = () => {
  count.value++;
};
const onClick2 = () => {
  count.value = count.value;
};
</script>

<template>
  <div>
    <h2>AsyncWatchEffect</h2>
    <p>Count: {{ count }}</p>
    <button @click="onClick">Increment</button>
    <button @click="onClick2">Same</button>
  </div>
</template>
