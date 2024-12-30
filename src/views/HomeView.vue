<script setup>
import Hero from '../components/Hero.vue';
import HomeCard from '../components/HomeCard.vue';
import JobListenings from '../components/JobListenings.vue';
</script>
<template>
    <Hero title="Welcome to Murads Vue.js example site" subtitle="Find the Vue job that fits your skills and needs"/>
    <HomeCard/>
    <JobListenings limit="3" :showButton="true"/>
</template>