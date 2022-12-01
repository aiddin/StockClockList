<!-- :simpleDate="simpleDate"
:simpleTime="simpleTime"
:simpleDateTime="simpleDateTime" -->
<template>
<div class="stockbg">
  <table>
    <tbody>
    <tr v-for="(persons) in persons" :key="persons.name">

      <td>{{persons.name}}</td>
      <td>{{persons.age}}</td>
      <td><tc-clock 
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
</style>