<template>
  <v-container>
    <transition name="slide" mode="out-in">
      <div v-if="mode == 'proc'" key="proc">
        <v-layout>
          <h2 style="padding-top: 10px;">Выберите процессор для материнской платы и нажмите кнопку </h2>
          <v-spacer></v-spacer>
          <v-btn @click.native="mode = 'mb'">Далее</v-btn>
        </v-layout>
        <v-layout wrap>
          <v-flex xs12 sm4 v-for="(val, i ) in processors" :key="i">
            <v-card style="margin: 15px;" :dark='val.chg' :style="val.chg ? 'transform:scale(1.05) rotate(2deg)' : ''">
              <v-img :src="val.src" aspect-ratio="2.75"></v-img>
              <v-card-title primary-title>
                <h2 class="headline mb-0">{{val.name}}</h2>
                <v-flex xs12>
                  <hr>
                </v-flex>
                <v-flex xs12>
                  Цена процессора:{{ val.price }}
                </v-flex>
                <v-flex xs12>
                  Частота процессора: {{ val.freq }}
                </v-flex>
                <v-flex>
                  Сокет материнской платы: {{ val.socket }}
                </v-flex>
              </v-card-title>
              <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn flat color="orange" @click="addProc(val)">{{ val.chg ? 'Снять': 'Выбрать'}}</v-btn>
              </v-card-actions>
            </v-card>
          </v-flex>
        </v-layout>
      </div>

      <div v-if="mode == 'mb'" key="'mb">
        <v-layout>
        <v-btn @click.native="mode = 'proc'" color="primary">Назад</v-btn>
        <v-spacer></v-spacer>
          <v-btn @click.native="mode = 'Ram'">Далее</v-btn>
          </v-layout>
        <v-layout>
          <h2 style="padding-top: 10px;">Подходящие под процессор материнские платы</h2>
          
        </v-layout>
        <v-layout wrap>
          <v-flex xs12 sm4 v-for="(val, i ) in mathB" :key="i" v-show="mathB">
            <v-card style="margin: 15px;" :dark='val.chg' :style="val.chg ? 'transform:scale(1.05) rotate(2deg)' : ''">
              <v-img :src="val.src" aspect-ratio="2.75"></v-img>
              <v-card-title primary-title>
                <h2 class="headline mb-0">{{val.name}}</h2>
                <v-flex xs12>
                  <hr>
                </v-flex>
                <v-flex xs12>
                  Цена материнской платы:{{ val.price }}
                </v-flex>
                <v-flex xs12>
                  Количество слотов под RAM: {{ val.slotRam }}
                </v-flex>
                <v-flex>
                  Сокет процессора: {{ val.socketForProc }}
                </v-flex>
              </v-card-title>
              <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn flat color="orange" @click="addProc(val)">{{ val.chg ? 'Снять': 'Выбрать'}}</v-btn>
              </v-card-actions>
            </v-card>
          </v-flex>
          <v-layout  style="margin-top:40px" justify-center v-show="!mathB" wrap row>
            <h1 style="color: gray">Ничего не найдено </h1>
            <v-flex d-flex justify-center xs12>
              <v-img src="http://cdn.onlinewebfonts.com/svg/img_87578.png" max-width='512'  contain></v-img>
            </v-flex>
          </v-layout>
        </v-layout>
      </div>

      <div v-if="mode == 'Ram'" key="Ram">
        <v-layout>
        <v-btn @click.native="mode = 'mb'" color="primary">Назад</v-btn>
        <v-spacer></v-spacer>
          </v-layout>
        <v-layout>
          <h2 style="padding-top: 10px;">Подходящие под материнскую плату Ram платы</h2>
          
        </v-layout>
        <v-layout wrap>
          <v-flex xs12 sm4 v-for="(val, i ) in ramC" :key="i" v-show="ramC">
            <v-card style="margin: 15px;" :dark='val.chg' :style="val.chg ? 'transform:scale(1.05) rotate(2deg)' : ''">
              <v-img :src="val.src" aspect-ratio="2.75"></v-img>
              <v-card-title primary-title>
                <h2 class="headline mb-0">{{val.name}}</h2>
                <v-flex xs12>
                  <hr>
                </v-flex>
                <v-flex xs12>
                  Цена оперативной платы:{{ val.price }}
                </v-flex>
                <v-flex xs12>
                   Слот RAM: {{ val.slotRam }}
                </v-flex>
              </v-card-title>
              <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn flat color="orange" @click="addProc(val)">{{ val.chg ? 'Снять': 'Выбрать'}}</v-btn>
              </v-card-actions>
            </v-card>
          </v-flex>
          <v-layout  style="margin-top:40px" justify-center v-show="!ramC" wrap row>
            <h1 style="color: gray">Ничего не найдено </h1>
            <v-flex d-flex justify-center xs12>
              <v-img src="http://cdn.onlinewebfonts.com/svg/img_87578.png" max-width='512'  contain></v-img>
            </v-flex>
          </v-layout>
        </v-layout>
      </div>
    </transition>
  </v-container>
</template>

<script>
  export default {
    data: () => ({
      mode: 'proc',
      processors: [{
          name: 'Intel core I7',
          price: '250',
          socket: 'LGA123',
          freq: '3.7',
          src: 'http://nbd.in.ua/_pu/10/59350265.jpg',
          chg: false
        },
        {
          name: 'Intel core I5',
          price: '170',
          socket: 'LRA523',
          freq: '3.5',
          src: 'https://avatars.mds.yandex.net/get-mpic/199079/img_id125385089808113823/9hq',
          chg: false
        },
        {
          name: 'Intel core I3',
          price: '150',
          socket: 'LGA455',
          freq: '2.8',
          src: 'https://i4.stat01.com/1/9732/97312493/afacdb/processor-intel-core-i7-7700k-oem.jpg',
          chg: false
        },
        {
          name: 'Intel core I3',
          price: '90',
          socket: 'LGA455',
          freq: '2.8',
          src: 'https://c.dns-shop.ru/thumb/st4/fit/wm/800/650/f39b7e0b4eae27f62e181648336a81f9/359b6a083843db2e76b2bf60ab9e72c36b53d3977449091026d7c76cf7276cc4.jpg',
          chg: false
        },
        {
          name: 'AMD Core S123',
          price: '130',
          socket: 'LRA523',
          freq: '4.2',
          src: 'https://avatars.mds.yandex.net/get-mpic/200316/img_id6518277650125732336/9hq',
          chg: false
        },
        {
          name: 'AMD Core S43',
          price: '100',
          socket: 'LGA123',
          freq: '3.5',
          src: 'data:image/jpeg;base64,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',
          chg: false
        },
        {
          name: 'AMD Core S123',
          price: '120',
          socket: 'LGA722',
          freq: '3.8',
          src: 'https://s.pn.com.ua/i/md/1041/2547917/2547917_00p.jpg',
          chg: false
        }
      ],
      matherboards: [{
          name: 'Asus rog 322sd',
          price: '2200',
          socketForProc: 'LGA722',
          slotRam: 'DDR4',
          src: 'https://avatars.mds.yandex.net/get-mpic/1244413/img_id8518687580170397326.jpeg/9hq',
          chg: false
        },
        {
          name: 'Asus rog524ghr',
          price: '1800',
          socketForProc: 'LGA123',
          slotRam: 'DDR4',
          src: 'https://avatars.mds.yandex.net/get-mpic/1363210/img_id150633614917168267.jpeg/9hq',
          chg: false
        },
        {
          name: ' GIGABYTE GA-AB350M',
          price: '2400',
          socketForProc: 'LGA455',
          slotRam: 'DDR3',
          src: 'https://avatars.mds.yandex.net/get-mpic/200316/img_id305151713786711767/9hq',
          chg: false
        },
        {
          name: 'GIGABYTE GA-A320M-H ',
          price: '1800',
          socketForProc: 'LGA123',
          slotRam: 'DDR4',
          src: 'https://avatars.mds.yandex.net/get-mpic/199079/img_id3087959540668683799/9hq',
          chg: false
        },
        {
          name: 'ASRock 970M Pro3',
          price: '1200',
          socketForProc: 'LGA123',
          slotRam: 'DDR3',
          src: 'https://avatars.mds.yandex.net/get-mpic/199079/img_id3087959540668683799/9hq',
          chg: false
        },
        {
          name: 'GIGABYTE GA-E3000N ',
          price: '1500',
          socketForProc: 'LRA523',
          slotRam: 'DDR3',
          src: 'https://avatars.mds.yandex.net/get-mpic/1382936/img_id5858964667538050497.jpeg/9hq',
          chg: false
        },
      ],
      ram: [{
          name: 'Samsung DDR4 2400 ',
          price: '2700',
          slotRam: 'DDR4',
          src: 'https://avatars.mds.yandex.net/get-mpic/397397/img_id7681616492752923633/9hq',
          chg: false
        },
        {
          name: 'Samsung DDR4 2666  ',
          price: '2800',
          slotRam: 'DDR4',
          src: 'https://avatars.mds.yandex.net/get-marketpic/208469/market_cJHWd8SrH6WG9gcw65j20Q/200x200',
          chg: false
        },
        {
          name: 'Hynix DDR4 2133 DIMM  ',
          price: '3000',
          slotRam: 'DDR4',
          src: 'https://avatars.mds.yandex.net/get-mpic/397397/img_id920176839949844433.jpeg/9hq',
          chg: false
        },
        {
          name: 'HyperX HX316C10FB/8',
          price: '1200',
          slotRam: 'DDR3',
          src: 'https://avatars.mds.yandex.net/get-mpic/1246680/img_id1516431781414565692.jpeg/9hq',
          chg: false
      },
        {
          name: 'HyperX HX316CфывB/8',
          price: '1300',
          slotRam: 'DDR3',
          src: 'https://avatars.mds.yandex.net/get-mpic/1246680/img_id1516431781414565692.jpeg/9hq',
          chg: false
        }
      ]
    }),
    methods: {
      addProc(val) {
        val.chg = !val.chg
      }
    },
    computed: {
      mathB (){
        let mas = []
         this.matherboards.forEach((element) => {
           this.processors.forEach((el) => {
              if (mas.some(item => {
                return item == element
            }) === false) {
              if (element.socketForProc == el.socket && el.chg) {
                mas.push(element)
              }
            }
         })
        })
        return mas.length>0  ?  mas : false
      },
      ramC () {
        let mas = []
         this.ram.forEach((element) => {
           this.matherboards.forEach((el) => {
              if (mas.some(item => {
                return item == element
            }) === false) {
              if (element.slotRam == el.slotRam && el.chg) {
                mas.push(element)
              }
            }
         })
        })
        return mas.length>0  ?  mas : false
      }
    }
  }
</script>

<style>
  .slide-enter-active,
  .slide-leave-active {
    transition: all .5s;
  }

  .slide-enter {
    transform: translateX(90%);
  }

  .slide-leave-to {
    transform: translateX(-90%);
    opacity: 0;
  }
</style>