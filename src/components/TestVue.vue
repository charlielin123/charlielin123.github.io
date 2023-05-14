<script setup>
import { computed,reactive } from 'vue';
import LightBoxBase from './LightBoxBase.vue';
const props = defineProps(['man','showLight']);
const emit = defineEmits(['changeVal','update:showLight']);
const show=computed({
    get:()=>{
        return props.showLight
    },
    set:(value)=>{
        emit('update:showLight',value)
    }
})
// const manComputed = computed({
//   get: () => {
//     return props.man;
//   },
//   set: (val) => {
//     console.log(val)
//     // emit('changeVal', val);
//   }
// });
const manComputed = reactive(props.man)

</script>

<template>
  <LightBoxBase v-model:show="show">
    <template #body>
      <div class="container" style="width: 600px">
        <div class="row my-1">
          <div class="col-4">ID:123</div>
          <div class="col-8">
            <input v-model="manComputed.id" />
          </div>
        </div>
        <div class="row my-1">
          <div class="col-4">姓名</div>
          <div class="col-8">
            <input type="text" v-model="manComputed.name" />
          </div>
        </div>
        <div class="row my-1">
          <div class="col-4">年紀</div>
          <div class="col-8">
            <input type="number" v-model="manComputed.age" />
          </div>
        </div>
        <div class="row my-1">
          <div class="col-4">AutoComplete</div>
          <div class="col-8">
            <input v-model="manComputed.select" />
          </div>
        </div>
      </div>
    </template>
  </LightBoxBase>
</template>

<style lang="scss" scoped></style>
