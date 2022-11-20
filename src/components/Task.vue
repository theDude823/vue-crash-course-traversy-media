<template>
  <div class="flex justify-between bg-red-400">
    <div :class="{ 'border-l-2 border-lime-500': task.reminder }">
      <p>{{ task.text }}</p>
      <p>{{ task.day }}</p>
    </div>
    <div class="flex gap-6">
      <button @click="$emit('checkClick', task.id)">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          fill="none"
          viewBox="0 0 24 24"
          stroke-width="1.5"
          stroke="currentColor"
          class="w-6 h-6 my-auto"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            d="M9 12.75 11.25 15 15 9.75M21 12a9 9 0 1 1-18 0 9 9 0 0 1 18 0z"
          />
        </svg>
      </button>
      <button @click="$emit('xClick', task.id)">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          fill="none"
          viewBox="0 0 24 24"
          stroke-width="1.5"
          stroke="currentColor"
          class="w-6 h-6 my-auto mr-5 text-red-800"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            d="M6 18 18 6M6 6l12 12"
          />
        </svg>
      </button>
    </div>
  </div>
</template>

<script setup>
const props = defineProps({ task: "Object" });
</script>

<style lang="scss" scoped></style>
