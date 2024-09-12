<script setup>
// ref is like the useState in react
import { ref, onMounted } from "vue";

const name = ref("John Doe");
const status = ref("active");
const tasks = ref(["Task One", "Task Two", "Task Three"]);
const newTask = ref("");

const toggleStatus = () => {
  if (status.value === "active") {
    status.value = "pending";
  } else if (status.value === "pending") {
    status.value = "inactive";
  } else {
    status.value = "active";
  }
};

const addTask = () => {
  if (newTask.value.trim() !== "") {
    tasks.value.push(newTask.value);
    newTask.value = "";
  }
};

onMounted(async () => {
  try {
    const response = await fetch("https://jsonplaceholder.typicode.com/todos", {
      method: "GET",
      headers: {
        "Content-Type": "application/json",
      },
    });
    const data = await response.json();
    console.log(data);
    tasks.value = data.map((task) => task.title);
  } catch (error) {
    throw error;
  }
});

const deleteTask = (index) => {
  tasks.value.splice(index, 1);
  // array.splice(start, deleteCount, item1, item2, ...)
  // start : The index at which to start changing the array. If greater than the length of the array, it will start at the end. If negative, it starts from the end of the array.
  // deleteCount : deleteCount: The number of elements to remove from the array, starting from the start index
  // item1 , item2 : the element that will be added after the start index
};
</script>

<template>
  <h1>{{ name }}</h1>
  <!-- To use v-if v-else-if v-else the HTML elements of those conditions should be stick together -->
  <div>
    <p v-if="status === 'active'">User is active</p>
    <p v-else-if="status === 'pending'">User is pending</p>
    <p v-else>User is not active</p>
  </div>

  <form @submit.prevent="addTask">
    <lable for="newTask">Add Task</lable>
    <input type="text" id="newTask" name="newTask" v-model="newTask" />
    <button type="submit">Submit</button>
  </form>

  <!-- Here is v-for which is used to iterate over the elements in the array -->
  <h3>Task :</h3>
  <ul>
    <div v-for="(task, index) in tasks" :key="task">
      <li>{{ task }}</li>
      <button @click="deleteTask(index)">x</button>
    </div>
  </ul>

  <!-- v-bind: is used to indicate that the attribute is dynamic, not static or string -->
  <a :href="link">Google</a>

  <!-- v-on: is like an event listener onClick which = method defined in the setup function -->
  <button v-on:click="toggleStatus">Change status</button>
</template>
