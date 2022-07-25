<template>
    <div class="block" :style="pose" v-if="showBlock" @click="stopTimer">
        click me
    </div>
</template>

<script>
export default {
    props: ['delay'],
    data() {
        return {
            pose: null,
            showBlock: false,
            timer: null,
            reactionTime: 0
        }
    },
    mounted() {
        setTimeout(() => {
            this.showBlock = true
            this.startTimer()
        },
         this.delay) 
    },
    methods: {
        startTimer() {  
              function range(start, end) {
                return[...Array(end + 1).keys()].filter(value => end >= value && start <= value );
            }
            var x = range(0, 200)
            var x2 = range(1, 200)
            for (var i in x2){
                x2[i] *= -1
                x.push(x2[i])
            }
            var y = range(0, 200)
            var randomx = x[Math.floor(Math.random()*x.length)]
            var randomy = y[Math.floor(Math.random()*y.length)]
            this.pose = `transform: translate(${randomx}%, ${randomy}%);`
            console.log(this.pose)

            this.timer = setInterval(() => {
                this.reactionTime += 10
            }, 10)
        },
        stopTimer() {
            clearInterval(this.timer)
            this.$emit('end', this.reactionTime) 
        }

    }
}
</script>

<style>
.block {
    width: 400px;
    border-radius: 20px;
    background: #0faf87;
    color: white;
    text-align: center;
    padding: 100px 0;
    margin: 40px auto;
}
</style>