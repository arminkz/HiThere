<script setup>
import { ref, onMounted } from "vue";

const name = ref("Armin");
const status = ref("active");
const tasks = ref(["Task 1", "Task 2", "Task 3"]);
const newTask = ref("");

const link = "https://www.google.com";

const toggleStatus = () => {
  status.value = status.value === "active" ? "inactive" : "active";
};

const addTask = () => {
  if (newTask.value.trim() !== "") {
    tasks.value.push(newTask.value);
    newTask.value = "";
  }
};

const deleteTask = (index) => {
  tasks.value.splice(index, 1);
};

onMounted (async () => {
  try {
    const response = await fetch("https://jsonplaceholder.typicode.com/todos");
    const data = await response.json();
    tasks.value = data.map((task) => task.title);
  } catch (error) {
    console.error(error);
  }
});
</script>

<template>
  <h1>Hello {{name}}</h1>
  <p v-if="status === 'active'">User is active</p>
  <p v-else-if="status === 'pending'">User is pending</p>
  <p v-else>User is inactive</p>

  <form @submit.prevent="addTask">
    <label for="newTask">Add Task</label>
    <input type="text" id="newTask" name="newTask" v-model="newTask" />
    <button type="submit">Add</button>
  </form>

  <h3>Tasks</h3>
  <ul>
    <li v-for="(task,index) in tasks" :key="task">
      <span>{{task}}</span>
      <button @click="deleteTask(index)">X</button>
    </li>
  </ul>

  <!-- <a v-bind:href="link">Google here!</a> -->
  <a :href="link">Google here!</a>
  <br>

  <!-- <button v-on:click="toggleStatus">Change Status</button> -->
  <button @click="toggleStatus">Change Status</button>
</template>

<style scoped>
h1 {
  color: red;
}
</style>
