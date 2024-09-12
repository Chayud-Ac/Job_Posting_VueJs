<script setup>
import Hero from "@/components/Hero.vue";
import HomeCards from "@/components/HomeCard.vue";
import JobListings from "@/components/JobListings.vue";
</script>

<template>
  <Hero />
  <HomeCards />
  <JobListings limit="3" />
</template>
