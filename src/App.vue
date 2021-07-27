<template>
<div class="sumupContainer">
  <h3>Total Time Spent</h3>
  <p class="totalTime">{{hours}} : {{minute}} : {{timeinsecond}}</p>
  <p></p>
</div>
<div class="timerTemplate" v-for="(len,index) in noOfTimer" v-bind:key="index">
  <timer v-on:timertoapp="onchildtimer"></timer>
</div>
<button class="addNewTimerButton" v-on:click="addNewTimer()">Add New Timer</button>
</template>

<script>
import Timer from './components/Timer.vue'
export default {
  name: 'App',
  components: {
    Timer
  },
  data(){
    return{
      noOfTimer:[1],
      count:1,
      timeinsecond:0,
      minute:0,
      seconds:0,
      hours:0
    }
  },
  mounted(){
    },
  methods:{
    addNewTimer(){
      this.count = this.count+2;
      this.noOfTimer.push(this.count);
    },
    onchildtimer(value){
      console.log('initiated onchildtimer'+ value);
      this.timeinsecond = value.sec;
      this.minute = value.mint;
      this.hours = value.hrs;
    }
  }
}
</script>

<style>
body{
  margin:0;
  padding:0;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.addNewTimerButton{
  height:30px;
  padding:5px 15px;
  border-radius: 5px;
  border:none;
  outline:none;
  color:white;
  background-color: #2e2e2e;
}
.sumupContainer{
  color:white;
  background-color: #2e2e2e;
  margin:0 0;
  padding:7px 0;
}
.sumupContainer h3{
  margin-bottom: 7px;
}
.sumupContainer p{
  margin-top: 0;
  font-weight: 700;
  font-size: 17px;
}
</style>
