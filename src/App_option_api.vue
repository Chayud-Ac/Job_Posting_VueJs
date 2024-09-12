<!-- option api -->

<script>
export default {
  data() {
    return {
      name: "Chayud Mahithiphark",
      status: "pending",
      tasksWithObjects: [
        { name: "Task One" },
        { name: "Task Two" },
        { name: "Task Three" },
      ],
      link: "https://google.com",
    };
  },
  methods: {
    toggleStatus() {
      if (this.status === "active") {
        this.status = "pending";
      } else if (this.status === "pending") {
        this.status = "inactive";
      } else {
        this.status = "active";
      }
    },
  },
};
</script>

<template>
  <h1>{{ name }}</h1>
  <!-- To use v-if v-else-if v-else the html element of those condition should be stick together -->
  <div>
    <p v-if="status === 'active'">User is active</p>
    <p v-else-if="status === 'pending'">User is pending</p>
    <p v-else>User is not active</p>
  </div>

  <!-- Here is v-for which use to iterate the element in the array -->
  <h3>Task :</h3>
  <ul>
    <li v-for="task in tasksWithObjects" :key="task">{{ task.name }}</li>
  </ul>
  <!-- v-bind: is use to tell that the artribute gonna be dynamic not static or string -->
  <!-- short hand is only : (but v-bind is prefered) -->
  <a :href="link">Google</a>
  <a v-bind:href="link">Google</a>

  <!-- onClick is like event listener onClick which = method that we define in export default object -->
  <!-- short hand is only : (but v-bind is prefered) -->

  <button v-on:click="toggleStatus">Change status</button>
  <button @click="toggleStatus">Change status</button>
</template>
