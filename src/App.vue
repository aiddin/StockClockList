<!-- :simpleDate="simpleDate"
:simpleTime="simpleTime"
:simpleDateTime="simpleDateTime" -->
<template>
<div>
  <tr>
    <th>
      
       
        <td><v-text>hehe</v-text></td>
        <tc-clock 
        
    :serverDate="serverDate" 
    :glow="glow"
   
    :simpleTime="simpleTime" 
    /></th>
    <th></th>
    <tc-clock 
    :serverDate="serverDate" 
    :glow="glow"
   
    :simpleTime="simpleTime" 
    />
    <br>
  </tr>
  <table>
    <tc-clock 
    :serverDate="serverDate" 
    :glow="glow"
   
    :simpleTime="simpleTime" 
    />
    <br>
  
    <tc-clock 
    :serverDate="serverDate" 
    :glow="glow"
   
    :advancedTime="advancedTime" 
    />
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