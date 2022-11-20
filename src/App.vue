<script setup>
// import TheWelcome from "./components/TheWelcome.vue";
import Header from "./components/Header.vue";
import Button from "./components/Button.vue";
import Tasks from "./components/Tasks.vue";
import AddTask from "./components/AddTask.vue";
import { ref, reactive } from "vue";

const showAddTask = ref(false);
// fetching from db.json; 2 functions are created but 1 function would do the task just fine
const tasks = ref("");
async function created() {
  tasks.value = await fetchTasks();
}
created();
async function fetchTasks() {
  const res = await fetch("http://localhost:5000/tasks/");
  const data = await res.json();
  return data;
}
//function to fetch each task individually:

async function fetchTask(id) {
  const res = await fetch(`http://localhost:5000/tasks/${id}`);
  const data = await res.json();
  return data;
}

const onClick = () => {
  showAddTask.value = !showAddTask.value;
};

const xClick = async (id) => {
  const res = await fetch(`http://localhost:5000/tasks/${id}`, {
    method: "DELETE",
  });
  //if deleted in backend, remove it in the front end, else show error deleting in backend
  res.status === 200
    ? (tasks.value = tasks.value.filter((task) => task.id !== id))
    : alert("error deleting task");
};

const checkClick = async (id) => {
  const taskToToggle = await fetchTask(id);
  const updateTask = { ...taskToToggle, reminder: !taskToToggle.reminder };

  const res = await fetch(`http://localhost:5000/tasks/${id}`, {
    method: "PUT",
    headers: {
      "Content-type": "application/json",
    },
    body: JSON.stringify(updateTask),
  });

  const data = await res.json();
  tasks.value = tasks.value.map((task) =>
    task.id === id ? { ...task, reminder: data.reminder } : task
  );
};

const addTask = async (newTask) => {
  const res = await fetch("http://localhost:5000/tasks", {
    method: "POST",
    headers: {
      "Content-type": "application/json",
    },
    body: JSON.stringify(newTask),
  });
  // this gives response of the task we added, from backend:
  const data = await res.json();
  //appends a data dict to "tasks"
  tasks.value = [...tasks.value, data];
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
