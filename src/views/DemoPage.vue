<script setup>
//@ts-check
import { ref, reactive, h,isVNode } from 'vue';
import { LightBoxBase } from '../components';
import { AutoComplete, autoCompleteConfig } from '../components/AutoComplete';

function _uuid() {
  var d = Date.now();
  if (typeof performance !== 'undefined' && typeof performance.now === 'function') {
    d += performance.now(); //use high-precision timer if available
  }
  return 'xxxxxxxx-xxxx-4xxx-yxxx-xxxxxxxxxxxx'.replace(/[xy]/g, function (c) {
    var r = (d + Math.random() * 16) % 16 | 0;
    d = Math.floor(d / 16);
    return (c === 'x' ? r : (r & 0x3) | 0x8).toString(16);
  });
}
const loading = ref(false);
const load = () => {
  loading.value = true;
};
const loaded = () => {
  loading.value = false;
};

class Man {
  id;
  name = '';
  age = 0;
  select = '';
  newObject = { name: '', id: null };
  constructor(name, age, select, newObject) {
    this.id = _uuid();
    this.name = name || '';
    this.age = age || null;
    this.select = select || '';
    this.newObject = newObject;
  }
}

/**

 * @type {import('vue').UnwrapNestedRefs<Man[]>}
 */
const manData = reactive([]);
const manReactive = reactive(new Man());
Object.assign(manData, [
  new Man('Charlie', 22, 'Sick', { name: 'Habana', id: 1 }),
  new Man('Allen', 21, 'Smart', { name: 'NO NO NO', id: 2 }),
  new Man('Jacky', 24, 'HandSome and smart', { name: 'I do not know', id: 22 }),
  new Man('Bruce', 28, 'HandSome', { name: 'I do not know', id: 22 })
]);

const showManBox = ref(false);
const getManApi = (manId) => {
  console.log('go');
  load();
  return new Promise((resolve) => {
    const t = setTimeout(() => {
      // console.log(manData);
      // console.log(number);
      const temp = manData.find((man) => man.id == manId);
      clearInterval(t);
      resolve(temp);
      loaded();
    }, 2000);
  });
};
const getMan = (manId) => {
  Object.assign(manReactive, { name: '', age: null, id: null, select: '' });
  manIdConfig.setDefaultData({ name: '', age: null, id: null, select: '' });
  if (manId == null) {
    if (testModel.value == 0) {
      showManBox.value = true;
    }
    return;
  }
  getManApi(manId).then((res) => {
    Object.assign(manReactive, res);
    manConfig.setDefaultData(res.select || '');
    manIdConfig.setDefaultData(res);
    if (testModel.value == 0) {
      showManBox.value = true;
    }
  });
};

const saveManApi = () => {
  console.log('doSave');
  load();
  return new Promise((resolve) => {
    const t = setTimeout(() => {
      console.log(manReactive.id);
      if (manReactive.id == null) {
        manReactive.id = _uuid();
      }
      /**
       * @type {Man|undefined}
       */
      const temp = manData.find((man) => {
        man.id == manReactive.id;
      });
      const index = temp ? manData.indexOf(temp) : -1;
      if (index == -1) {
        const temp = Object.assign({}, manReactive);
        manData.push(temp);
        loaded();
        resolve(manReactive);
        return;
      }

      Object.assign(manData[index], manReactive);
      console.log(temp);
      clearInterval(t);
      resolve(temp);
      loaded();
    }, 500);
  });
};

const saveMan = () => {
  saveManApi().then(() => {
    alert('成功');
  });
  showManBox.value = false;
  console.log(manReactive);
};

function searchSelectListAPI(searchKey) {
  return new Promise((resolve) => {
    // load()
    const t = setTimeout(() => {
      const manList = manData.filter((man) => {
        return man.select.startsWith(searchKey);
      });
      const res = manList.map((man) => {
        return man.select;
      });
      resolve(res);
      clearTimeout(t);
      // loaded()
    }, 2500);
  });
}

// const autoTrigger = ref(false);
const manConfig = autoCompleteConfig(searchSelectListAPI);
const testModel = ref(0);
const changeModel = () => {
  if (testModel.value == 0) {
    testModel.value = 1;
    return;
  }
  testModel.value = 0;
};
const test1 = () => {
  console.log(manReactive.id);
  getMan(manIdConfig.result ? manIdConfig.result.id : 0);
};
const getIdListApi = (input) => {
  return new Promise((resolve) => {
    const t = setTimeout(() => {
      const manList = manData.filter((man) => {
        return man.id.startsWith(input);
      });
      // const res = manList.map((man) => {
      //   return man.id
      // })
      console.log(manList);
      // console.log(res)
      clearTimeout(t);
      resolve(manList);
    }, 5000);
  });
};
const manIdConfig = autoCompleteConfig(getIdListApi);
manIdConfig.propertyName = 'id';
const title = ref('');
const abc = ref();
const testFun = (index) => {
  title.value = 'title' + index;
  if (index == 3) {
    abc.value=h('button', {class:"btn btn-success",innerHTML: '下載' ,href:"/asd"});
    console.log(isVNode(abc.value))
  }
};
</script>

<template>
  <div class="demo">
    <div class="loading" v-show="loading">
      <div>
        <h1>Loading....</h1>
      </div>
    </div>
    <LightBoxBase v-model:show="showManBox">
      <template #title>{{ title }}</template>
      <template #body>
        <div class="container" style="width: 600px">
          <div class="row my-1">
            <div class="col-4">ID</div>
            <div class="col-8">
              <AutoComplete
                v-model="manReactive"
                :config="manIdConfig"
                v-model:result="manIdConfig.result"
                :changeFunction="test1"
              />
            </div>
          </div>
          <div class="row my-1">
            <div class="col-4">姓名</div>
            <div class="col-8">
              <input type="text" v-model="manReactive.name" />
            </div>
          </div>
          <div class="row my-1">
            <div class="col-4">年紀</div>
            <div class="col-8">
              <input type="number" v-model="manReactive.age" />
            </div>
          </div>
          <div class="row my-1">
            <div class="col-4">AutoComplete</div>
            <div class="col-8">
              <AutoComplete v-model="manReactive.select" :config="manConfig" />
            </div>
          </div>
        </div>
      </template>
      <template #footer>
        <button class="btn btn-warning" @click="saveMan()">save</button>
      </template>
    </LightBoxBase>
    <div>
      <h2 v-if="!abc">測試頁面</h2>
      <abc v-if="abc"/>
    </div>
    <div class="container">
      <div class="row">
        <div class="col-4 btn-box">
          <div class="row">
            <div class="col">
              <button
                class="btn"
                :class="testModel == 0 ? 'btn-success' : 'btn-primary'"
                @click="changeModel"
              >
                燈箱/非燈箱切換
              </button>
            </div>
          </div>

          <template v-for="(man, index) in manData" :key="man.id">
            <div class="row">
              <div class="col">
                <button class="btn btn-success" @click="getMan(man.id), testFun(index)">
                  {{ man.name }}
                </button>
              </div>
            </div>
          </template>
          <div class="row">
            <div class="col">
              <button class="btn btn-success" @click="getMan()">新增</button>
            </div>
          </div>
        </div>
        <div class="col-8">
          <div class="container">
            <div class="row" v-show="testModel == 1">
              <div class="container text-white bg-dark my-2" style="width: 600px">
                <div>
                  <div class="container" style="width: 600px">
                    <div class="row my-1">
                      <div class="col-4">ID</div>
                      <div class="col-8">
                        <AutoComplete
                          v-model="manReactive"
                          :config="manIdConfig"
                          :changeFunction="test1"
                        />
                      </div>
                    </div>
                    <div class="row my-1">
                      <div class="col-4">姓名</div>
                      <div class="col-8">
                        <input type="text" v-model="manReactive.name" />
                      </div>
                    </div>
                    <div class="row my-1">
                      <div class="col-4">年紀</div>
                      <div class="col-8">
                        <input type="number" v-model="manReactive.age" />
                      </div>
                    </div>
                    <div class="row my-1">
                      <div class="col-4">AutoComplete</div>
                      <div class="col-8">
                        <!-- <AutoComplete v-model="manReactive.select" :config="manConfig" /> -->
                      </div>
                    </div>
                  </div>
                </div>
                <div
                  class="my-4"
                  style="display: flex; align-items: center; justify-content: center"
                >
                  <button class="btn btn-warning" @click="saveMan()">save</button>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.loading {
  display: flex;
  position: fixed;
  z-index: 99999999;
  width: 100vw;
  height: 100vh;
  background-color: rgba(255, 255, 255, 0.544);
  justify-content: center;
  align-items: center;
  h1 {
    color: black;
  }
}
.demo {
  width: 100vw;
  height: 100vh;
  // background-color: rgb(73, 73, 73);
}
.btn-box {
  .row {
    padding: 0.5rem;
  }
}
</style>
