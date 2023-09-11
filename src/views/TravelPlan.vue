<script setup>
import { reactive, computed } from 'vue';
const totalPay = (/** @type {{ transportation: { option: any[]; }; }} */ target) => {
  const payList = target.transportation.option.map((i) => i.pay);
  return payList.reduce((acc, cur) => acc + cur);
};
const totalWalkingTime = (/** @type {{ transportation: { option: any[]; }; }} */ target) => {
  const walkList = target.transportation.option.map(
    (/** @type {{ mode: string; time: any; }} */ i) => {
      return i.mode == 'walking' ? i.time : 0;
    }
  );
  return walkList.reduce((/** @type {any} */ acc, /** @type {any} */ cur) => acc + cur) + '分鐘';
};
const totalTime = (/** @type {{ transportation: { option: any[]; }; }} */ target) => {
  const walkList = target.transportation.option.map((/** @type {{ time: any; }} */ i) => i.time);
  return walkList.reduce((/** @type {any} */ acc, /** @type {any} */ cur) => acc + cur) + '分鐘';
};
const plan = reactive([
  [
    {
      name: '成田國際機場',
      arrivedTime: '12:25',
      leaveTime: '13:30',
      transportation: {
        googleUrl: 'https://goo.gl/maps/iK3Rz4cWL2md9gWu5',
        option: [
          {
            mode: 'Sky liner',
            trainName: '付費特急(往京成上野)',
            to: '日暮里',
            pay: 1300,
            time: 41
          },
          {
            mode: 'walking',
            trainName: null,
            to: null,
            pay: 0,
            time: 3
          },
          {
            mode: 'JR',
            trainName: '山手線(內環線)',
            to: '新大久保',
            pay: 180,
            time: 20
          },
          {
            mode: 'walking',
            trainName: null,
            to: 'APA酒店',
            pay: 0,
            time: 10
          }
        ]
      }
    },
    {
      name: 'APA酒店',
      arrivedTime: '15:00',
      leaveTime: '15:30',
      transportation: {
        googleUrl: 'https://goo.gl/maps/3dXGdYD6giR9pU6y8',
        option: [
          {
            mode: 'walking',
            trainName: null,
            to: '東新宿',
            pay: 0,
            time: 10
          },
          {
            mode: '地鐵',
            trainName: '副都心線(往元町、中華街)',
            to: '澀谷車站',
            pay: 180,
            time: 9
          },
          {
            mode: 'walking',
            trainName: null,
            to: '澀谷LOFT',
            pay: 0,
            time: 2
          }
        ]
      }
    },
    {
      name: '澀谷LOFT',
      arrivedTime: '16:00',
      leaveTime: '17:25',
      transportation: {
        googleUrl: 'https://goo.gl/maps/NP8NMFUKyZxqryT18',
        option: [
          {
            mode: 'walking',
            trainName: null,
            to: '澀谷Sky',
            pay: 0,
            time: 6
          }
        ]
      }
    },
    {
      name: '澀谷Sky',
      arrivedTime: '17:40',
      leaveTime: '20:00',
      transportation: {
        googleUrl: 'https://goo.gl/maps/Z4Az5rEvpHsuRfiw6',
        option: [
          {
            mode: 'walking',
            trainName: null,
            to: '澀谷車站',
            pay: 0,
            time: 1
          },
          {
            mode: '地鐵',
            trainName: '副都心線(往石神井公園)',
            to: '東新宿',
            pay: 180,
            time: 9
          }
        ]
      }
    },
    {
      name: 'APA酒店',
      arrivedTime: '20:20',
      leaveTime: '',
      transportation: null
    },
    {
      name: '新宿晃晃',
      arrivedTime: '',
      leaveTime: '',
      transportation: null
    }
  ],
  [
    {
      name: 'APA酒店',
      arrivedTime: '',
      leaveTime: '6:45',
      transportation: {
        googleUrl: 'https://goo.gl/maps/d7SSShCkvXW2yFLcA',
        option: [
          {
            mode: 'walking',
            trainName: null,
            to: '東新宿',
            pay: 0,
            time: 8
          },
          {
            mode: '地鐵',
            trainName: '都營大江戶線(往飯田橋、兩國)',
            to: '月島',
            pay: 0,
            time: 31
          },
          {
            mode: 'walking',
            trainName: '轉乘',
            to: '月島',
            pay: 0,
            time: 4
          },
          {
            mode: '地鐵',
            trainName: '有樂町線(往新木場)',
            to: '新木場',
            pay: 320,
            time: 7
          },
          {
            mode: 'walking',
            trainName: '轉乘',
            to: '新木場',
            pay: 0,
            time: 8
          },
          {
            mode: 'JR',
            trainName: '武藏野線(往西船橋)',
            to: '舞濱',
            pay: 170,
            time: 6
          }
        ]
      }
    },
    {
      name: '東京迪士尼',
      arrivedTime: '7:50',
      leaveTime: '20:00',
      transportation: {
        googleUrl: 'https://goo.gl/maps/7JMbQJT1WKRbjWqR8',
        option: [
          {
            mode: 'JR',
            trainName: '武藏野線(往東京)',
            to: '新木場',
            pay: 167,
            time: 6
          },
          {
            mode: 'walking',
            trainName: '轉乘',
            to: '新木場',
            pay: 0,
            time: 4
          },
          {
            mode: '地鐵',
            trainName: '有樂町線(往和光市)',
            to: '飯田橋',
            pay: 0,
            time: 23
          },
          {
            mode: 'walking',
            trainName: '轉乘',
            to: '飯田橋',
            pay: 0,
            time: 8
          },
          {
            mode: '地鐵',
            trainName: '都營大江戶線(往都廳前[折返])',
            to: '東新宿',
            pay: 317,
            time: 8
          },
          {
            mode: 'walking',
            trainName: '',
            to: 'APA酒店',
            pay: 0,
            time: 8
          }
        ]
      }
    },
    {
      name: 'APA酒店',
      arrivedTime: '21:00',
      leaveTime: '',
      transportation: null
    }
  ],
  [
    {
      name: 'APA酒店',
      arrivedTime: '00:00',
      leaveTime: '08:00',
      transportation: {
        googleUrl: 'https://goo.gl/maps/bpkxTEpaQrDXBwSAA',
        option: [
          {
            mode: 'walking',
            trainName: null,
            to: 'blue bottle',
            pay: 0,
            time: 14
          }
        ]
      }
    },
    {
      name: 'blue bottle 新宿店',
      arrivedTime: '08:20',
      leaveTime: '09:00',
      transportation: {
        googleUrl: 'https://goo.gl/maps/x2QaM6KPrQr2nuJn7',
        option: [
          {
            mode: 'walking',
            trainName: null,
            to: '新宿',
            pay: 0,
            time: 6
          },
          {
            mode: '地鐵',
            trainName: '中央‧總武線各站停車',
            to: '淺草橋',
            pay: 360,
            time: 6
          },
          {
            mode: 'walking',
            trainName: null,
            to: '淺草橋',
            pay: 0,
            time: 3
          },
          {
            mode: '地鐵',
            trainName: '淺草線',
            to: '淺草',
            pay: 0,
            time: 2
          },
          {
            mode: 'walking',
            trainName: null,
            to: '淺草寺 雷門',
            pay: 0,
            time: 5
          }
        ]
      }
    },
    {
      name: '風神雷門 (去淺草站放行李)',
      arrivedTime: '09:45',
      leaveTime: '10:40',
      transportation: {
        googleUrl: '',
        option: [
          {
            mode: 'walking',
            trainName: null,
            to: '淺草',
            pay: 0,
            time: 6
          },
          {
            mode: 'walking',
            trainName: '淺草線',
            to: '押上',
            pay: 0,
            time: 3
          }
        ]
      }
    },
    {
      name: '晴空塔',
      arrivedTime: '10:55',
      leaveTime: '11:50',
      transportation: {
        googleUrl: '',
        option: [
          {
            mode: '地鐵',
            trainName: '淺草線',
            to: '東銀座',
            pay: 320,
            time: 6
          },
          {
            mode: 'walking',
            trainName: null,
            to: '東銀座',
            pay: 0,
            time: 1
          },
          {
            mode: '地鐵',
            trainName: '各站停車中目黑',
            to: '日比谷',
            pay: 0,
            time: 2
          },
          {
            mode: 'walking',
            trainName: null,
            to: 'Shake Shack - 東京國際論壇店',
            pay: 0,
            time: 5
          }
        ]
      }
    },
    {
      name: 'shack shark',
      arrivedTime: '12:10',
      leaveTime: '13:40',
      transportation: {
        googleUrl: '',
        option: [
          {
            mode: 'walking',
            trainName: null,
            to: '有樂町',
            pay: 0,
            time: 4
          },
          {
            mode: '地鐵',
            trainName: '山手線',
            to: '東京車站',
            pay: 180,
            time: 3
          },
          {
            mode: 'walking',
            trainName: null,
            to: '東京車站',
            pay: 0,
            time: 4
          },
          {
            mode: '新幹線',
            trainName: '希望號',
            to: '新大阪',
            pay: 180,
            time: 150
          },
          {
            mode: '地鐵',
            trainName: '御堂筋線',
            to: '心齋橋站',
            pay: 180,
            time: 3
          },
          {
            mode: 'walking',
            trainName: null,
            to: '大阪心齋橋相鐵FRESA INN',
            pay: 0,
            time: 6
          }
        ]
      }
    },
    {
      name: '大阪心齋橋相鐵FRESA INN',
      arrivedTime: '17:15',
      leaveTime: '00:00',
      transportation: null
    }
  ],
  [
    {
      name: '大阪心齋橋相鐵FRESA INN',
      arrivedTime: '00:00',
      leaveTime: '07:10',
      transportation: {
        googleUrl: 'https://goo.gl/maps/fsRJAD4xLHVDcP3fA',
        option: [
          {
            mode: '地鐵',
            trainName: null,
            to: '大阪環球影城',
            pay: 410,
            time: 32
          }
        ]
      }
    },
    {
      name: '大阪環球影城',
      arrivedTime: '08:00',
      leaveTime: '20:00',
      transportation: {
        googleUrl: 'https://goo.gl/maps/rycmHA5U36zkz8Yi6',
        option: [
          {
            mode: '地鐵',
            trainName: null,
            to: '大阪心齋橋相鐵FRESA INN',
            pay: 430,
            time: 33
          }
        ]
      }
    },
    {
      name: '大阪心齋橋相鐵FRESA INN',
      arrivedTime: '20:40',
      leaveTime: '',
      transportation: null
    },
    {
      name: '大阪晃晃',
      arrivedTime: '20:40',
      leaveTime: '',
      transportation: null
    }
  ],
  [
    {
      name: '大阪心齋橋相鐵FRESA INN',
      arrivedTime: '00:00',
      leaveTime: '08:00',
      transportation: {
        googleUrl: '',
        option: [
          {
            mode: '地鐵',
            trainName: null,
            to: '新世界本通商店街',
            pay: 190,
            time: 15
          }
        ]
      }
    },
    {
      name: '新世界本通商店街&通天閣',
      arrivedTime: '08:15',
      leaveTime: '10:20',
      transportation: {
        googleUrl: '',
        option: [
          {
            mode: '地鐵',
            trainName: null,
            to: '大阪城',
            pay: 240,
            time: 35
          }
        ]
      }
    },
    {
      name: '大阪城',
      arrivedTime: '10:55',
      leaveTime: '13:30',
      transportation: {
        googleUrl: '',
        option: [
          {
            mode: '地鐵',
            trainName: null,
            to: '大阪城',
            pay: 240,
            time: 31
          }
        ]
      }
    },
    {
      name: '梅田阪急百貨',
      arrivedTime: '10:55',
      leaveTime: '13:30',
      transportation: {
        googleUrl: '',
        option: [
          {
            mode: '地鐵',
            trainName: null,
            to: '大阪城',
            pay: 240,
            time: 35
          }
        ]
      }
    },
  ]
]);
const show = reactive({});
const showTran = (/** @type {string | number} */ day, /** @type {string | number} */ index) => {
  show[day] = show[day] ?? {};
  show[day][index] = !show[day][index];
};

const totalTransPay = (/** @type {string} */ mode) => {
  const a = [];
  plan.forEach((i) =>
    i.forEach((j) =>
      j.transportation?.option.forEach((d) => {
        if (d.mode == mode) {
          a.push(d.pay);
        }
      })
    )
  );
  const total = a.reduce((a, b) => a + b);
  return total;
};
const transTools = computed(() => {
  const list = [];
  plan.forEach((i) =>
    i.forEach((j) =>
      j.transportation?.option.forEach((d) => {
        if (!list.includes(d.mode)) list.push(d.mode);
      })
    )
  );

  return list;
});
</script>

<template>
  <div>
    <template v-for="item in transTools" :key="item">
      <div>{{ item }} ： ¥{{ totalTransPay(item) }}</div>
    </template>

    <div class="wrap mt-3">
      <div class="container">
        <div class="row">
          <template v-for="(targets, day) in plan" :key="targets">
            <div class="col-12 col-lg-6 my-3">
              <h4>Day{{ day + 1 }}:</h4>
              <template v-for="(target, index) in targets" :key="target.name">
                <div class="tt1 mt-3 p-2">
                  <div class="container">
                    <div class="row">
                      <div class="col-7 d-flex" style="align-items: center">
                        <div class="m-0 h5">
                          {{ target.name }}
                        </div>
                      </div>
                      <div class="col-5" style="font-size: 0.5rem; text-align: end">
                        抵達：{{ target.arrivedTime }} <br />
                        離開：{{ target.leaveTime }}
                      </div>
                    </div>
                  </div>
                </div>
                <div class="transportation" v-if="target.transportation">
                  <div class="container my-2">
                    <h5
                      class=""
                      style="text-align: center; font-size: 1rem"
                      @click="showTran(day, index)"
                    >
                      交通：¥{{ totalPay(target) }} <span class="walkImg"></span
                      >{{ totalWalkingTime(target) }} 共
                      {{ totalTime(target) }}
                      <br />
                    </h5>
                    <div class="d-flex" style="justify-content: center">
                      <a
                        style="text-align: center"
                        target="_blank"
                        :href="target.transportation.googleUrl"
                      >
                        連結</a
                      >
                    </div>
                    <div class="transportationContent" v-show="show?.[day]?.[index]">
                      <div class="row header" style="background-color: aliceblue">
                        <div class="col col-4 col-lg-2">交通方式</div>
                        <div class="col col-4 col-lg-2">時間</div>
                        <div class="col col-4 col-lg-2">價格</div>
                        <div class="col col-12 col-lg-3">車種</div>
                        <div class="col col-12 col-lg-3">目的</div>
                      </div>
                      <template v-for="item in target.transportation.option" :key="item">
                        <div class="row">
                          <div class="col col-4 col-lg-2">{{ item.mode }}</div>
                          <div class="col col-4 col-lg-2">{{ item.time }}min</div>
                          <div class="col col-4 col-lg-2">¥{{ item.pay }}</div>
                          <div class="col col-12 col-lg-3">
                            {{ item.trainName }}
                          </div>
                          <div class="col col-12 col-lg-3">{{ item.to }}</div>
                        </div>
                      </template>
                    </div>
                  </div>
                </div>
              </template>
            </div>
          </template>
        </div>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.tt1 {
  border: rgb(207, 255, 136) 3px solid;
  border-radius: 0.5rem;
  &:hover {
    background-color: rgb(240, 250, 250);
  }
}
.transportation {
  margin: 0.5rem 1rem;
  border: 1px solid rgba(80, 80, 116, 0.5);
  &:hover {
    background-color: rgba(125, 125, 179, 0.1);
  }

  .row {
    // border: solid 0.1rem;

    &:nth-child(odd) {
      background-color: rgba(97, 134, 102, 0.3);
      &:hover {
        background-color: rgba(97, 134, 102, 0.6);
      }
    }
    &:nth-child(even) {
      background-color: rgba(148, 154, 218, 0.3);
      &:hover {
        background-color: rgba(148, 154, 218, 0.6);
      }
    }

    .col {
      text-align: center;
      border-radius: 0;
      border: solid 0.1rem;
    }
    .col-2 {
      border-radius: 0;
      border: solid 0.1rem;
    }
  }
}
.walkImg {
  display: inline-block;
  position: relative;
  top: -1px;
  background-image: url(https://maps.gstatic.com/consumer/images/icons/1x/directions_walk_grey650_24dp.png);
  background-size: cover;
  width: 1rem;
  aspect-ratio: 1/1;
  margin-right: -2px;
  vertical-align: middle;
}
</style>
