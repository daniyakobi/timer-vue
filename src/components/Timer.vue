<template>
    <div class="timer">
        <h3>Таймер №{{ index + 1 }}:</h3>
        <div class="timer__block">{{ currentTime }}</div>
        <div class="timer__text text" v-if="currentTime == 0">{{ msg }}</div>
    </div>
</template>

<script>
    export default {
        name: "Timer",
        props: {
            time: {
                type: Number,
            },
            index: {
                type: Number
            }
        },
        data() {
            return {
                msg: '',
                interval: null,
                currentTime: null
            }
        },
        methods: {
            timer(time) {
                this.currentTime = time
                this.interval  = setInterval(() => {
                    if (this.currentTime <= 0) {
                        clearInterval(this.interval)
                        this.finishHandler(this.time)
                    } else {
                        this.currentTime = (this.currentTime - 0.1).toFixed(3)
                    }
                }, 100)
            },
            finishHandler(time) {
                this.msg = `Прошло секунд: ${time}`
            }
        },
        mounted() {
            this.timer(this.time)
        }
    }
</script>

<style scoped>
  .timer {
      display: flex;
      align-items: center;
      padding-bottom: 10px;
      border-bottom: 1px solid #333;
      width: 100%;
      margin-top: 25px;
  }
  .timer h3 {
      margin: 0;
      font-size: 24px;
      line-height: 30px;
      margin-right: 25px;
  }
  .timer__block {
      font-weight: bold;
      font-size: 24px;
      line-height: 30px;
      margin-right: 25px;
  }
  .timer__text {
      margin-right: 0;
      margin-left: auto;
  }
</style>