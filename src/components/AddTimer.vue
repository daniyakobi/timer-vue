<template>
    <div id="add-timer">
        <form>
            <h2>Создание таймера:</h2>
            <div class="input-group">
                <input class="input" v-model="time" type="text" name="time" />
                <span>секунд</span>
            </div>
            <button class="button" @click.prevent="createTimer">Создать таймер</button>
            <button class="button" @click.prevent="clearTimers">Очистить список</button>
        </form>
        <div class="error text" v-if="err.length > 0">{{ err }}</div>
    </div>
</template>

<script>
    export default {
        name: "AddTimer",
        data() {
            return {
                time: null,
                err: ''
            }
        },
        methods: {
            createTimer() {
                const re = /^-?\d+\.?\d*$/
                if (re.test(this.time)) {
                    this.err = ''
                    this.$emit('add-timer',{
                        id: Date.now(),
                        time: +this.time
                    })
                    this.time = null
                } else {
                    this.time = null
                    this.err = 'Введите число!'
                }
            },
            clearTimers() {
                this.err = ''
                this.$emit('clear-timers')
            }
        }
    }
</script>

<style>
    #add-timer {
        margin-bottom: 30px;
    }
    #add-timer form {
        display: flex;
        align-items: center;
    }
    #add-timer h2 {
        margin: 0;
        margin-right: 25px;
        font-size: 35px;
        line-height: 50px;
    }
    .input-group {
        display: flex;
        align-items: center;
    }
    .input {
        width: 50px;
        height: 50px;
        outline: none;
        font-size: 24px;
        line-height: 30px;
        padding: 0 10px;
        text-align: center;
    }
    .input-group span {
        margin-left: 10px;
        font-size: 24px;
        line-height: 30px;
    }
    .button {
        margin-left: auto;
        margin-right: 0;
        display: flex;
        align-items: center;
        justify-content: center;
        height: 50px;
        padding: 0 25px;
        background-color: transparent;
        border: 1px solid #333;
        color: #333;
        font-size: 24px;
        line-height: 30px;
        cursor: pointer;
        transition: all 0.3s linear;
    }
    .button:hover {
        background-color: #333;
        color: #fff;
    }
    .error {
        color: red;
    }
</style>