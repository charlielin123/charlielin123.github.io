<script setup lang="ts">
import { reactive, inject, ref } from 'vue';
import axios from 'axios';

const temp = inject("test") as {
    name: string,
    age: number
};

const a = ref(18);
const b = ref("fuck");

defineExpose({
    a,
    b
})


</script>



<template>
    <div>
        <h3>{{ temp.name }}</h3>
        {{ a }}
    </div>
</template>



<style lang="scss" scoped></style>