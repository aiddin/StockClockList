<!-- :simpleDate="simpleDate"
:simpleTime="simpleTime"
:simpleDateTime="simpleDateTime" -->
<template>
<div class="stockbg">
  <table>
  <tr>
    <th>Company</th>
    <th>Contact</th>
    <th>Country</th>
  </tr>
  <tr>
    <td>Alfreds Futterkiste</td>
    <td>Maria Anders</td>
    <td>Germany</td>
  </tr>
  <tr>
    <td>Centro comercial Moctezuma</td>
    <td>Francisco Chang</td>
    <td>Mexico</td>
  </tr>
  <tr>
    <td v-text="message"></td>
    <td>Roland Mendel</td>
    <td>Austria</td>
  </tr>
  <tr>
    <td>Island Trading</td>
    <td>Helen Bennett</td>
    <td>UK</td>
    <td><tc-clock 
    :serverDate="serverDate" 
    :glow="glow"
    :advancedTime="advancedTime" 
    /></td>
  </tr>
  
 
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
    };
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
  background-color: #000000;
  
}
</style>