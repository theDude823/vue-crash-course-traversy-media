<script setup>
// import TheWelcome from "./components/TheWelcome.vue";
import Header from "./components/Header.vue";
import Button from "./components/Button.vue";
import Tasks from "./components/Tasks.vue";
import AddTask from "./components/AddTask.vue";
import { ref, reactive } from "vue";

const showAddTask = ref(false);
const tasks = ref([
  {
    id: "1",
    text: "Doctors Appointment",
    day: "March 5th at 2:30pm",
    reminder: true,
  },
  {
    id: "2",
    text: "Meeting with boss",
    day: "March 6th at 1:30pm",
    reminder: true,
  },
  {
    id: "3",
    text: "Food shopping",
    day: "March 7th at 2:00pm",
    reminder: false,
  },
]);
const onClick = () => {
  showAddTask.value = !showAddTask.value;
};

const xClick = (id) => {
  // this deletes the selected task
  tasks.value = tasks.value.filter((task) => task.id !== id);
};

const checkClick = (id) => {
  // this changes reminder
  tasks.value = tasks.value.map((task) =>
    task.id === id ? { ...task, reminder: !task.reminder } : task
  );
};
const addTask = (newTask) => {
  //appends a new task dict to "tasks"
  tasks.value = [...tasks.value, newTask];
};
</script>

<template>
  <header>
    <div
      class="flex flex-col w-4/5 max-w-md p-10 mx-auto border-2 border-red-400 mt-14"
    >
      <div class="flex justify-between">
        <Header
          @buttonClick="onClick"
          :showAddTask="showAddTask"
          title="Task Tracker"
        />
      </div>
      <AddTask v-show="showAddTask" @addTask_emit="addTask" />
      <div class="flex-1 w-full bg-gray-400">
        <Tasks @checkClick="checkClick" @xClick="xClick" :tasks="tasks" />
      </div>
    </div>
  </header>

  <main></main>
</template>
