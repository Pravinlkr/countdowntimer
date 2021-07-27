<template>
    <button class="startButton" v-on:click="startTimer()" v-if="!timerStart">Start</button>
    <button class="resetButton" v-if="needReset" v-on:click="resetTimer()">Reset</button>
    <button class="stopButton" v-on:click="stopTimer()">Stop</button>
</template>
<script>
export default {
    name:'Control',
    props:{
        stopTimer:Function,
        startTimer:Function,
        resetTimer:Function,
        timerStart:Boolean,
        needReset:Boolean
    }
}
</script>
<style scoped>
button{
    height: 100px;
    width: 100px;
    border-radius: 50%;
    margin:1% 3%;
    font-size: 20px;
    border:none;
    outline:none;
    color:white;
}
button.startButton{
    background-color: #43a876;
}
button.stopButton{
    background-color: #274752;
}
button.resetButton{
    background-color: #40b3db;
}
</style>