<template>
  <div>
    <button @click="$emit('buttonClick')" class="">{{ text }}</button>
  </div>
</template>

<script setup>
const props = defineProps(["text"]);
</script>
