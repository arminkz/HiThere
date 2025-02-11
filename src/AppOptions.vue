<script>
export default {
  data() {
    return {
      name: "Armin",
      status: 'pending',
      tasks: ['Task 1', 'Task 2', 'Task 3'],
      link: 'https://www.google.com'
    }
  },
  methods: {
    toggleStatus() {
      this.status = this.status === 'active' ? 'inactive' : 'active';
    }
  }
}
</script>

<template>
  <h1>Hello {{name}}</h1>
  <p v-if="status === 'active'">User is active</p>
  <p v-else-if="status === 'pending'">User is pending</p>
  <p v-else>User is inactive</p>

  <h3>Tasks</h3>
  <ul>
    <li v-for="task in tasks" :key="task">{{task}}</li>
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
