<template>
  <div>
    <div
      class="mt-3 border-2 border-black"
      v-for="task in tasks"
      :key="task.id"
    >
      <Task @checkClick="checkClick" @xClick="xClick" :task="task" />
    </div>
  </div>
</template>

<script setup>
import Task from "../components/Task.vue";
const props = defineProps({ tasks: "Array" });
const emit = defineEmits(["xClick", "checkClick"]);
const xClick = (id) => {
  emit("xClick", id);
};
const checkClick = (id) => {
  emit("checkClick", id);
};
</script>

<style lang="scss" scoped></style>
//$emit('dblclick_', task.id)
