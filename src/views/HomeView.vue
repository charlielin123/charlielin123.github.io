<script setup lang="ts">
import TheWelcome from '../components/TheWelcome.vue'
import LoginView from '@/views/LoginView.vue'
import { ref, watch, type Ref } from 'vue';

const pop:Ref = ref(null);

// const a=await pop.value;
// console.log(b);
watch(pop, () => {

  if (pop.value != null) {

    if (pop.value.a && pop.value.b) {
      const a = pop.value.a;
      const b = pop.value.b;
    }

  }

})
const fun1 = () => {

  if(pop.value != null) pop.value.a += "13";
}


</script>

<template>
  <main>
    <TheWelcome />
    <!-- {{ a }} -->
    <LoginView ref="pop" />
    <button @click="fun1">dddddddd</button>
  </main>
</template>
