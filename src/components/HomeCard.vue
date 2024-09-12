<script setup>
import Card from "@/components/Card.vue";

const arrayOfCards = [
  {
    title: "For Developers",
    description: "Browse our Vue jobs and start youe career today",
    href: "/jobs",
  },
  {
    title: "For Recruiter",
    description: "Browse our Vue jobs and start youe career today",
    href: "/jobs",
  },
];
</script>

<template>
  <section class="py-4">
    <div class="container-xl lg:container m-auto">
      <div class="grid grid-cols-1 md:grid-cols-2 gap-4 p-4 rounded-lg">
        <Card
          v-for="(card, index) in arrayOfCards"
          :key="card.href"
          :title="card.title"
          :description="card.description"
          :href="card.href"
          :color="`${index === 1 && 'bg-green-100'}`"
        />
      </div>
    </div>
  </section>
</template>
