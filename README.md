# Job_posting_VueJs

This project is a Job Posting web application built with Vue 3 and Vite. This aim to be based project that learning all fundamental thing in developing web application using VueJS including project structure , Page routing , Vue components , Vue lifecycle method. In this project we aim to mainly focus on the Vue so the backend I use the JSON Web Server to mock a backend server for handle http request (GET , POST , PUT , DELETE). Using the tailwind css for styling

# Key feature

- **Job View**: User allow to view jobs post
- **Job Posting:**: User allow to post job and provided information about the job and company
- **Job Edit:**: User allow to edit the specific job that has posted
- **Job delete**: User allow to delete the specific job

## Project Structure src/

- **assets/**: Static assets
- **components/**: Vue components (storing all reusable component that can be apply across the project)ได้
- **views/**: Application views (storing all view component that basically act like a page.)
- **assets/**: Static assets
- **router/index.js**: Vue Router setup (setting page route including static and dynamic page)
- **App.vue**: Main app component (apply component that will show in every page or apply the main layout of the app and include the <RouterView /> )
- **main.js**: Application entry point (setting up the vue app)

# Fundamental things to know about VueJs

## Vue using Virtual DOM and component base structure similar to reactJS which each component can also take in props as well.

### Example of creating reusable component in Vue using **Composition API** Card component. This very similar to ReactJS

```vue
<script setup>
import { defineProps } from "vue";
import { RouterLink } from "vue-router";

defineProps({
  // we call the function defineProps which use to create the Props that this component will take in which each prop can be defined extra property like type , required , default
  title: {
    type: String,
    required: true,
  },
  description: {
    type: String,
    default: "Jobs describtion here",
  },
  href: {
    type: String,
    required: true,
  },
  color: {
    type: String,
    default: "bg-gray-100",
  },
});
</script>

<template>
  <div v-bind:class="`${color}  bg-gray-100 p-6 rounded-lg shadow-md `">
    <h2 class="text-2xl font-bold">{{ title }}</h2>
    <p class="mt-2 mb-4">{{ description }}</p>
    <RouterLink
      v-bind:to="href"
      class="inline-block bg-black text-white rounded-lg px-4 py-2 hover:bg-gray-700"
    >
      Browse Jobs
    </RouterLink>
  </div>
</template>
```

## Two Different Ways to Create Components in Vue.js

Vue.js provides two primary ways to create components: the **Options API** and the **Composition API**. Below are examples for both. For those who just move from react I recommended using **Composition API** will take less learning curve to understand. The script tag can place at the top ot bottom of the component depending on ypu preference. For me I personally like to place at the top

### 1. Options API Example:

```vue
<script>
export default {
  data() {
    // store state variable
    return {
      jobTitle: "",
      companyName: "",
      submittedJob: null,
    };
  },
  methods: {
    submitJob() {
      this.submittedJob = {
        jobTitle: this.jobTitle,
        companyName: this.companyName,
      };
    },
  },
};
</script>

<template>
  <div>
    <!-- just normal html element  -->
    <h2>Post a Job</h2>
    <form @submit.prevent="submitJob">
      <label for="jobTitle">Job Title:</label>
      <input v-model="jobTitle" id="jobTitle" />
      <label for="companyName">Company Name:</label>
      <input v-model="companyName" id="companyName" />
      <button type="submit">Submit</button>
    </form>

    <div v-if="submittedJob">
      <h3>Job Posted:</h3>
      <p><strong>Title:</strong> {{ submittedJob.jobTitle }}</p>
      <p><strong>Company:</strong> {{ submittedJob.companyName }}</p>
    </div>
  </div>
</template>
```

### 1. Composition API Example:

```vue
<script setup>
import { defineProps } from "vue";
import { RouterLink } from "vue-router";

defineProps({
  title: {
    type: String,
    required: true,
  },
  description: {
    type: String,
    default: "Jobs describtion here",
  },
  href: {
    type: String,
    required: true,
  },
  color: {
    type: String,
    default: "bg-gray-100",
  },
});
</script>

<template>
  <div v-bind:class="`${color}  bg-gray-100 p-6 rounded-lg shadow-md `">
    <h2 class="text-2xl font-bold">{{ title }}</h2>
    <p class="mt-2 mb-4">{{ description }}</p>
    <RouterLink
      v-bind:to="href"
      class="inline-block bg-black text-white rounded-lg px-4 py-2 hover:bg-gray-700"
    >
      Browse Jobs
    </RouterLink>
  </div>
</template>
```

## Basic and Commonly Used Vue Directives (v-) and Event Modifiers (@)

### Commonly used Vue directives (v-);

- **v-if / v-else-if / v-else** - conditional rendering

```vue
<script setup>
import { ref } from "vue";

const isLogin = ref(true);
</script>

<template>
  <!-- conditional render the div depenging on the isLogin state -->
  <!-- the html block element should be stick together to conditional render and use v-if , v-else-if , v-else -->
  <div v-if="isLoggedIn">Welcome, user!</div>
  <div v-else>Login to continue.</div>
</template>
```

- **v-for** - use to map the to render a list of element (like .map() in javascript) instead we can directly apply v-for to the component we want to iterate and display a list of that component

```vue
<script setup>
import { ref } from "vue";

const isLogin = [{ name: "YOYO" }, { name: "YEYE" }];
</script>

<template>
  <ul>
    <li v-for="(item, index) in items" :key="item.index">{{ item.name }}</li>
  </ul>
</template>
```

## Two important APIs used to create reactive data

- **ref()**: used to create a reactive reference to both primitives (numbers, strings, booleans) or objects. this return an object that has .value property that we can access to them or change the value of it.

```vue
<script setup>
import { ref } from "vue";

const count = ref(0);
const handleIncrementCount = () => {
  count.value++; // access the  state value and increment the value
};
</script>

<template>
  <!-- show the state value  -->
  <div>{{ count.value }}</div>
  <button @click="handleIncrementCount">Increment</button>
</template>
```

- **reactive()**: Use to create reactive object only accept object (non-primitive value) as a intial state and the state change can't be replace by new object , we have to manually change each key of the object.

```vue
<script setup>
import { reactive } from "vue";
// define the object state that take has keys of count and name
const state = reactive({
  count: 0,
  name: "Vue",
});

const handleIncrementCount = () => {
  state.count++; // access the  state value and increment the value
};
</script>

<template>
  <!-- show the state value  -->
  <div>{{ state.count }}</div>
  <div>{{ state.name }}</div>
  <button @click="handleIncrementCount">Increment</button>
</template>
```

- In comparison to react. Just Imagine that ref() and reactive() are the useState in react that we use to create the state in the component. ref() can be use with both primative value and non-primative value which has .value property that can be accessed or changed. while reactive() is only used for object
