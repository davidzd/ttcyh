<template>
  <div id="app" @click="changeImg">
    <waterfall :line="line" :align="align" :line-gap="width" :min-line-gap="80" :max-line-gap="100" :single-max-width="200" ref="waterfall" :watch="items">
      <waterfall-slot :class="item.slotClass" v-for="(item, index) in items" :width="50" :height="50" :order="index" :key="item.index">
        <img style=" max-width: 100%; max-height: 100%;" :src="item.photo">
      </waterfall-slot>
    </waterfall>
  </div>
</template>

<script>
  import Waterfall from 'vue-waterfall/lib/waterfall.vue'
  import WaterfallSlot from 'vue-waterfall/lib/waterfall-slot.vue'

  export default {
    components: {
      Waterfall,
      WaterfallSlot,
    },
    name: 'app',
    data() {
      return {
        width: 80,
        n: 0,
        line: 'h',
        align: 'center',
        items: [],
      }
    },
    created() {
      this.items = this.generate(500);
    },
    mounted() {
      setInterval(() => {
//        if (this.n <= this.items.length - 1) {
//          this.items[this.n] = {
//            photo: 'static/' + String(parseInt(Math.random() * 15 + 1)) + '.jpg',
//            slotClass: "animated flipInX"
//          };
//          this.n += 1;
//        } else {
//          this.n = 0;
//        }
        this.restart();
      }, 2000)
    },
    methods: {
      generate: function (n) {
        let items = [];
        for (let i=0; i<n; i++){
          items.push({
            photo: 'static/' + String(parseInt(Math.random() * 15 + 1)) + '.jpg',
            slotClass: (Math.random() > 0.5) ? "animated flipInX" : "animated flipInY"
          });
        }
        return items;
      },
      changeImg: function () {
        this.restart()
      },
      restart: function () {
        this.items = [];
        this.items = this.generate(500);
      }
    }
  }
</script>

<style>
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
  }
</style>
