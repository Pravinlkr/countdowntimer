<template>
    <h3>Count Down Timer</h3>
    <p class="timer"><span v-if="hours < 10">0</span>{{hours}} : <span v-if="minutes < 10">0</span>{{minutes}} : <span v-if="timeinms < 10">0</span>{{timeinms}}</p>
    <control :needReset="needReset" :timerStart="isStart" :stopTimer="stopTimer" :startTimer="startTimer" :resetTimer="resetTimer" />
</template>
<script>
import Control from './Control.vue'
export default {
    name:'Timer',
    components: {
        Control
    },
    data(){
        return{
            isStart:false,
            needReset:false,
            hours: 0,
            minutes:0,
            seconds:0,
            timeinms:0
        }
    },
    mounted(){
        //this.coverTimeInMs();
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
            this.isStart = false;
            this.needReset = true;
            clearInterval(this.seconds);
        },
        startTimer(){
            if(!this.isStart){
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
        }
    }
}
</script>
<style scoped>
p.timer{
    font-size: 35px;
    font-weight: 800;
}
</style>