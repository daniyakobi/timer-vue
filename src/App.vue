<template>
  <div id="app">
    <add-timer @add-timer="createTimer" @clear-timers="clearTimer" />
    <div v-if="timers.length > 0">
      <div class="timers" v-for="(item, index) in timers" :key="item.id">
        <timer :time="item.time" :index="index"/>
      </div>
    </div>
    <div class="text" v-else="">Таймеров пока нет!</div>
  </div>
</template>

<script>

import AddTimer from "@/components/AddTimer";
import Timer from "@/components/Timer";

export default {
  name: 'App',
  components: { Timer, AddTimer },
  data() {
    return {
      timers: []
    }
  },
  methods: {
    createTimer(timer) {
      this.timers.push({
        id: timer.id,
        time: timer.time
      })
    },
    clearTimer() {
      this.timers = []
    }
  }
}
</script>

<style>
  #app {
    max-width: 1000px;
    margin: auto;
    padding: 50px 0;
  }
  .text {
    font-size: 18px;
    line-height: 24px;
  }
</style>
