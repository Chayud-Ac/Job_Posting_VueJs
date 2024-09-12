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
