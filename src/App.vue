<template>
<div class="sumupContainer">
  <h3>Total Time Spent</h3>
  <p class="totalTime"><span v-if="hours < 10">0</span>{{hours}} : <span v-if="minute < 10">0</span>{{minute}} : <span v-if="timeinsecond < 10">0</span>{{timeinsecond}}</p>
</div>
<!--add timer component in main app-->
<div class="timerTemplate" v-for="(len,index) in noOfTimer" v-bind:key="index">
  <timer v-on:timertoapp="onchildtimer" :indexNo="index"></timer>
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
      hours:0,
      totalTimeCalArray:[],
      resultArray:[]
    }
  },
  mounted(){
    },
  methods:{
    addNewTimer(){
      this.count = this.count+2;
      this.noOfTimer.push(this.count);
    },
    onchildtimer(value, indexno){
      this.timeinsecond = value.sec;
      this.minute = value.mint;
      this.hours = value.hrs;
      console.log(this.totalTimeCalArray);
      this.replaceValueInArray(indexno, this.totalTimeCalArray, this.noOfTimer, {hrs:this.hours, mint:this.minute, sec:this.timeinsecond});
      this.fetchTotalTime(this.totalTimeCalArray, this.totalTimeCalArray.length, this.resultArray);

      //store result value in second minute and hours
      this.timeinsecond = this.resultArray[0].secnd;
      this.minute = this.resultArray[0].minut;
      this.hours = this.resultArray[0].hors;
      
      //updata minute after 59 second and hours after 59 minute
      if(this.timeinsecond > 59){
        this.minute = this.minute +1;
        this.timeinsecond = 0;
      }
      if(this.minute > 59){
        this.hours = this.hours+1;
        this.minute = 0;
        this.timeinsecond =0;
      }
    },
    replaceValueInArray(indexno, arr, originalarr, data){
      var i = 0;
      for(i=0; i<originalarr.length; i++){
        arr[indexno] = data;
      }
    },
    fetchTotalTime(arr,len, resultArray){
      var i=0;
      var minut=0;
      var secnd=0;
      var hors=0;
      for(i=0; i<len; i++){
        hors = hors+arr[i].hrs;
        minut = minut+arr[i].mint;
        secnd = secnd + arr[i].sec;
      }
      resultArray[0]={hors,minut,secnd};
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
