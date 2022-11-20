<template>
  <div class="my-3 border-2 border-red-700">
    <form @submit.prevent="onSubmit">
      <div class="">
        <label for="Task" class="">Task</label> <br />
        <input
          type="text"
          v-model="task"
          class="w-full rounded-md"
          id="Task"
        /><br />
      </div>
      <div class="mt-3">
        <label for="Day_Time" class="m">Day & Time</label> <br />
        <input
          type="text"
          v-model="day"
          class="w-full rounded-md"
          id="Day_Time"
        />
      </div>
      <div class="flex items-center justify-between mt-3 border-2 border-black">
        <label for="Reminder">Set Reminder</label>
        <input
          id="Reminder"
          v-model="reminder"
          class="mr-[50%] mb-1"
          type="checkbox"
        />
      </div>
      <div class="flex items-center justify-center">
        <button
          class="w-full px-3 py-2 mt-3 text-white bg-gray-900 border-2 border-black"
        >
          Save Task
        </button>
      </div>
    </form>
  </div>
</template>

<script setup>
import { ref } from "vue";
const task = ref("");
const day = ref("");
const reminder = ref("false");
const emit = defineEmits(["addTask_emit"]);
const onSubmit = () => {
  //validation
  if (!task.value) {
    alert("Please add a task");
    return;
  }
  const newTask = {
    id: Math.floor(Math.random() * 100000),
    task: task.value,
    day: day.value,
    reminder: reminder.value,
  };
  // emit upwards with the "newTask"
  const addTask_emit = () => {
    emit("addTask_emit", newTask);
  };
  addTask_emit();
  // initializing value after submission
  task.value = "";
  day.value = "";
  reminder.value = "false";
};
</script>

<style lang="scss" scoped></style>
