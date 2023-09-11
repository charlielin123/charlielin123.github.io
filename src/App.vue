<script setup lang="ts">
import DemoPage from './views/DemoPage.vue'
import TravelPlan from './views/TravelPlan.vue'
import testA from './components/testB.vue';
import {ref} from 'vue';
//@ts-check
// const a=ref('2002/12/12')
const a=ref('')
</script>

<template>
  <TravelPlan />
  <testA v-model="a"/>
</template>

<style scoped></style>
