<!-- :simpleDate="simpleDate"
:simpleTime="simpleTime"
:simpleDateTime="simpleDateTime" -->
<template>
<div class="stockbg">
  <table class ="huh">
    <tbody>
    <tr v-for="(exch) in exch" :key="exch.status">

      <td class="tdstyle" :style="testchange">{{exch.status}}</td>
      <td class="tdstyle">{{exch.name}}</td>
      <td class="tdstyle"><tc-clock 
        :serverDate="serverDate" 
        :glow="glow"
        :simpleTime="simpleTime" 
        /></td>
    </tr>
  </tbody>

 
  
  
  
 
  </table>
</div>
 
</template>
<script>
import TcClock from './components/TcClock.vue'
const date = new Date();

export default {
  name: 'App',
  components: { 
    TcClock,
  },
  data() {
    return {
      message: 'Hello this is GeeksforGeeks.',
      glow:'',
      serverDate: date,
      simpleTime: true,
      simpleDate: true,
      simpleDateTime: true,
      advancedTime: true,
      exch: [
          {name: 'Malaysia Exchange (MYX)', status: 1},
          {name: 'Indonesia Exchange (IDX)', status: 2},
          {name: 'Hong Kong Exchange (HKEX)', status: 3},
          {name: 'Singapore Exchange (SGX)', status: 1}
    ],
    }
  },
  
  computed:{
    testchange() {
      if (this.exch.status == 1) {
      console.log(this.exch.status);
      return {
        // "color": "blue"

      }
    }
      else
       
      console.log(this.exch.status);
        return {
         
          "text-shadow": "0 0 20px rgb(39, 83, 149), 0 0 20px rgba(10, 175, 230, 0)",
          color: "green",
          
        };
    },
  },
  methods: {
    setDateTime() {
      const date = new Date();

      this.serverDate = date;
      this.glow = '';
      this.simpleDate = true;
      this.simpleTime = true;
      this.simpleDateTime = true;
      this.advancedTime = true;
      
    },
  },

  mounted() {
    setInterval(() => {
      this.setDateTime();
    }, 0);
  },
};
</script>
<style>
.stockbg{
  background-color: #2b2b2b;
  
}
.tdstyle{
  
  color: #fff;
  
  font-weight: 600;
  margin : 150vw;
  padding: 50px;
  font-size :5vh;
  font-family: Oxygen, monospace;
}
.huh{
  margin: 0 auto;
  padding: 50px;
}
</style>