<template>
    <div class="timerBody" v-if="isToShowTimer">
        <button class="removeTimer" v-on:click="hideTimer()">X</button>
        <h3>Count Down Timer</h3>
        <p class="timer"><span v-if="hours < 10">0</span>{{hours}} : <span v-if="minutes < 10">0</span>{{minutes}} : <span v-if="timeinms < 10">0</span>{{timeinms}}</p>
        <control :isToStop="isToStop" :needReset="needReset" :timerStart="isStart" :stopTimer="stopTimer" :startTimer="startTimer" :resetTimer="resetTimer" />
    </div>
    
</template>
<script>
import Control from './Control.vue'
export default {
    name:'Timer',
    components: {
        Control
    },
    props:{
        /*removeTimer:Function,
        indexOfTimer:Number*/
    },
    data(){
        return{
            isStart:false,
            needReset:false,
            isToStop:false,
            isToShowTimer:true,
            hours: 0,
            minutes:0,
            seconds:0,
            timeinms:0,
            timerflag:0
        }
    },
    mounted(){
        this.emitTimerToParent();
    },
    methods:{
        coverTimeInMs(){
            this.seconds = setInterval(function(){
            this.timeinms = this.timeinms + 1;
            if(this.timeinms>59){
                this.minutes = this.minutes +1;
                this.timeinms = 0;
            }
            if(this.minutes>59){
                this.hours = this.hours+1;
                this.minutes = 0;
                this.timeinms = 0;
            }
            }.bind(this),1000);
        },
        stopTimer(){
            this.isToStop = false;
            this.isStart = false;
            this.needReset = true;
            clearInterval(this.seconds);
        },
        startTimer(){
            if(!this.isStart){
                this.isToStop = true;
                this.isStart = true;
                this.needReset = true;
                this.coverTimeInMs();
            }   
        },
        resetTimer(){
            this.hours = 0;
            this.minutes = 0;
            this.timeinms = 0;
            this.stopTimer();
            this.needReset = false;
            this.isToStop = false;
        },
        hideTimer(){
            this.isToShowTimer=false;
            clearInterval(this.seconds);
        },
        emitTimerToParent(){
            this.timerflag = setInterval(function(){
            this.$emit('timertoapp', {sec:this.timeinms,mint:this.minutes,hrs:this.hours});
            }.bind(this),1000);
            //{sec:this.timeinms,mint:this.minutes,hrs:this.hours}
        }
    }
}
</script>
<style scoped>
.timerBody{
    width:60%;
    margin:1% auto;
    height: auto;
    border:1px solid #ccc;
}
p.timer{
    font-size: 35px;
    font-weight: 800;
}
button.removeTimer{
    float:right;
    margin:10px 10px;
    border:none;
    outline:none;
    background-color: red;
    color:white;
}
</style>