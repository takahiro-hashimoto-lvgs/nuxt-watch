<script setup lang="ts">
const count = ref(0); // watchで明示的に監視対象としてしている
const unwatch_count = ref(0);　// watchEffectのコールバック内にある
const unwatched_count_nodep = ref(0); // watchEffectのコールバック内にない

watch(
    count,
    () => {
      console.log('AsyncWatch', 'count', count.value, 'unwatch_count', unwatch_count.value);
    },
    {
      immediate: false,
    }
);
const onClick = async () => {
  setTimeout(() => {
    count.value++;
    console.log('AsyncWatch didIncrement', 'count', count.value);
  }, 3000);
};
const onClickSame = () => {
  setTimeout(() => {
    count.value = count.value;
    console.log('AsyncWatch didSame', 'count', count.value);
  }, 1000);
};
const onClickSame2 = () => {
  setTimeout(() => {
    count.value++;
    count.value--;
    console.log('AsyncWatch didSame2', 'count', count.value);
  }, 1000);
};
const onClick3 = async () => {
  setTimeout(() => {
    count.value+=2;
    console.log('AsyncWatch didIncrement2', 'count', count.value);
  }, 1000);
};
const onUnwatchClick = async () => {
  setTimeout(() => {
    unwatch_count.value++;
    console.log('AsyncWatch unwatched didIncrement', 'unwatch_count', unwatch_count.value);
  }, 1000);
};
const onUnwatchNpDepClick = async () => {
  setTimeout(() => {
    unwatched_count_nodep.value++;
    console.log('AsyncWatch unwatched_count_nodep didIncrement', 'unwatched_count_nodep', unwatched_count_nodep.value);
  }, 1000);
};
</script>

<template>
  <div>
    <h2>AsyncWatch</h2>
    <p>Count: {{ count }}</p>
    <p>UnwatchCount: {{ unwatch_count }}</p>
    <button @click="onClick">Increment</button>
    <button @click="onClick3">Increment2</button>
    <button @click="onClickSame">Same</button>
    <button @click="onClickSame2">Same2</button>
    <button @click="onUnwatchClick">Unwatch</button>
    <button @click="onUnwatchNpDepClick">UnwatchNoDep</button>
  </div>
</template>
