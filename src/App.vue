<!-- :simpleDate="simpleDate"
:simpleTime="simpleTime"
:simpleDateTime="simpleDateTime" -->
<template>
<div class="stockbg">
  <table class ="huh">
    <tbody>
    <tr v-for="(persons) in persons" :key="persons.name">

      <td class="tdstyle">{{persons.name}}</td>
      <td class="tdstyle">{{persons.age}}</td>
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
      persons: [
          {name: 'Max', age: 20},
          {name: 'Jan', age: 30},
          {name: 'Ana', age: 40}
    ],
    }
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
  font-size: 20px;
  font-weight: 600;
  margin : 150vw;
  padding: 50px;
}
.huh{
  margin: 0 auto;
  padding: 50px;
}
</style>