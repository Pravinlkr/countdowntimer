<template>
<div class="timerTemplate" v-for="(len,index) in noOfTimer" v-bind:key="index">
  <timer ></timer>
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
      count:1
    }
  },
  methods:{
    addNewTimer(){
      this.count = this.count+2;
      this.noOfTimer.push(this.count);
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 30px;
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
.removeTimer{
  float:right;

}
</style>
