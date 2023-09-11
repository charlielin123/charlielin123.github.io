<script>
// @ts-check
// 使用普通的 <script> 来声明选项
export default {
  inheritAttrs: false
};
</script>

<script setup>
import moment from 'moment';
import testA from './testA.vue';
import { computed, onMounted, ref } from 'vue';
const props = defineProps({
  modelValue: {
    type: String
  }
});
const emit = defineEmits(['update:modelValue']);

const d = computed({
  get() {
    if (!props.modelValue) return new Date();
    const d = new Date(moment(props.modelValue).format('YYYY-MM-DD'));
    return d;
  },
  set(val) {
    emit('update:modelValue', moment(val).format('YYYY-MM-DD'));
  }
});

const d2 = ref(new Date());

const dateString = computed(() => {
  if (!props.modelValue) return '';
  return moment(props.modelValue).format('YYYY-MM-DD');
});
const test = (e) => {
  const target = e.target;
  const value = target.value;
  d2.value = new Date(moment(value).format('YYYY-MM-DD'));
  if (value.length < 10) return;
  emit('update:modelValue', moment(d2.value).format('YYYY-MM-DD'));
};
onMounted(() => {
  if(props.modelValue){
    d2.value = new Date(moment(props.modelValue).format('YYYY-MM-DD'));
  }
})
</script>

<template>
  <div style="border: solid">
    <input type="text" name="" id=""  @input="test" :="$attrs" />
    <testA v-model="d2" />
  </div>
</template>

<style lang="scss" scoped></style>
