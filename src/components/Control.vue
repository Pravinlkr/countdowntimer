<template>
    <button class="startButton" v-on:click="startTimer()" v-if="!timerStart">Start</button>
    <button class="resetButton" v-if="needReset" v-on:click="resetTimer()">Reset</button>
    <button class="stopButton" v-on:click="stopTimer()" v-if="isToStop">Stop</button>
</template>
<script>
export default {
    name:'Control',
    props:{
        stopTimer:Function,
        startTimer:Function,
        resetTimer:Function,
        timerStart:Boolean,
        needReset:Boolean,
        isToStop:Boolean
    }
}
</script>
<style scoped>
button{
    height: 70px;
    width: 70px;
    border-radius: 50%;
    margin:1% 3%;
    font-size: 17px;
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
button.addCounterButton{
    background-color: teal;
}
</style>