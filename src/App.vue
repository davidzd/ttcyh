<template>
  <div id="app" @click="changeImg">
    <waterfall :line="line" :align="align" :line-gap="50" :min-line-gap="100" :max-line-gap="100" :single-max-width="200" ref="waterfall" :watch="items">
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
        n: 0,
        line: 'h',
        align: 'center',
        items: [],
        isBusy: true
      }
    },
    created() {
      this.restart()
    },
    mounted() {
      setInterval(() => {
        if (this.n <= this.items.length - 1) {
          this.items[this.n].slotClass = "shake-slow shake-constant shake-constant--hover";
          this.n += 1;
        } else {
          this.n = 0;
        }
      }, 300)
    },
    methods: {
      generate: function () {
        this.items.push({
          photo: 'static/' + String(parseInt(Math.random() * 15 + 1)) + '.jpg',
          slotClass: "animated flipInX"
        });
      },
      changeImg: function () {
        this.restart();
      },
      restart: function () {
        this.n = 0;
        this.items = [];
        for (let i = 0; i < 1000; i++) {
          this.generate()
        }
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
