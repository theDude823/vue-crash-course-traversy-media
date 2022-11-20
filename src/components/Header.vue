<template>
  <h1 class="p-3 font-bold bg-blue-300">{{ title }}</h1>

  <Button
    class="p-3"
    @buttonClick="$emit('buttonClick')"
    :class="{
      'bg-green-400': showAddTask,
      'bg-red-400': !showAddTask,
    }"
    text="Add task"
  />
</template>

<script setup>
import Button from "./Button.vue";
const props = defineProps(["title", "showAddTask"]);
</script>
