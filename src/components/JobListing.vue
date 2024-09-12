<script setup>
import { defineProps, ref, computed } from "vue";
import { RouterLink } from "vue-router";

const props = defineProps({
  title: {
    type: String,
    required: true,
  },
  type: {
    type: String,
    required: true,
  },
  location: {
    type: String,
    required: true,
  },
  description: {
    type: String,
    required: true,
  },
  salary: {
    type: String,
    required: true,
  },
  company: {
    type: Object,
    required: true,
  },
  id: {
    type: Number,
  },
});

const showFullDescription = ref(false);

const truncatedDescription = computed(() => {
  let description = props.description;
  if (!showFullDescription.value) {
    description = description.slice(0, 100) + "...";
  }
  return description;
});

const toggleFullDescription = () => {
  showFullDescription.value = !showFullDescription.value;
};
</script>

<!-- 
{
    "title": "Senior Vue Dev",
    "type": "Full-Time",
    "location": "Boston, MA",
    "description": "We are seeking a talented Front-End Developer to join our team in Boston, MA. The ideal candidate will have strong skills in HTML, CSS, and JavaScript, with experience working with modern JavaScript frameworks such as Vue or Angular.",
    "salary": "$90K - $100K",
    "company": {
      "name": "NewTek Solutions",
      "description": "NewTek Solutions is a leading technology company specializing in web development and digital solutions. We pride ourselves on delivering high-quality products and services to our clients while fostering a collaborative and innovative work environment.",
      "contactEmail": "contact@teksolutions.com",
      "contactPhone": "555-555-5555"
    },
    "id": "1"
  }, -->

<template>
  <div class="bg-white rounded-xl shadow-md relative">
    <div class="p-4">
      <div class="mb-6">
        <div class="text-gray-600 my-2">{{ type }}</div>
        <h3 class="text-xl font-bold">{{ title }}</h3>
      </div>

      <div class="mb-5">
        <div>
          {{ truncatedDescription }}
        </div>
        <button
          class="text-green-500 hover:text-green-600 mb-5"
          @click="toggleFullDescription"
        >
          {{ showFullDescription ? "less" : "more" }}
        </button>
      </div>

      <h3 class="text-green-500 mb-2">${{ salary }}/ Year</h3>

      <div class="border border-gray-100 mb-5"></div>

      <div class="flex flex-col lg:flex-row justify-between mb-4">
        <div class="text-orange-700 mb-3">
          <i class="pi pi-map-marker text-orange-700"></i>
          {{ location }}
        </div>
        <RouterLink
          v-bind:to="`/jobs/${id}`"
          class="h-[36px] bg-green-500 hover:bg-green-600 text-white px-4 py-2 rounded-lg text-center text-sm"
        >
          Read More
        </RouterLink>
      </div>
    </div>
  </div>
</template>
