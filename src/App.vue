<!-- :simpleDate="simpleDate"
:simpleTime="simpleTime"
:simpleDateTime="simpleDateTime" -->
<template>
<tc-clock 
        :serverDate="serverDate" 
        :glow="glow"
        :advancedTime="advancedTime" 
      
> </tc-clock>
 
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
      exch: [
          {id:'MYX', name: 'Malaysia Exchange (MYX)', status: '1', gmTime: '+8'},
          {id:'IDX',name: 'Indonesia Exchange (IDX)', status: '2', gmTime: '+7'},
          {id:'HKEX',name: 'Hong Kong Exchange (HKEX)', status: '3', gmTime: '+8'},
          {id:'SGX',name: 'Singapore Exchange (SGX)', status: '1', gmTime: '+8'},// 1 hour == 3,600,000 milliseconds
    ],
    }
  },
  
  computed:{
    // testchange() {
    //   if (this.exch.status == 1) {
    //   console.log(this.exch.status);
    //   return {
    //     // "color": "blue"

    //   }
    // }
    //   else
       
    //   console.log(this.exch.status);
    //     return {
         
    //       "text-shadow": "0 0 20px rgb(39, 83, 149), 0 0 20px rgba(10, 175, 230, 0)",
    //       color: "green",
          
    //     };
    // },
  },
  methods: {
    setDateTime() {
      this.glow = '';
      this.simpleDate = true;
      this.simpleTime = true;
      this.simpleDateTime = true;
      this.advancedTime = true;
      
    },
    setServerDate() {
      const date = new Date();
      
      console.log (-date.getTimezoneOffset()/60+'heh')//get utc time offset
     date.setHours(date.getHours() + (-1) );
      this.serverDate = date;
    },
  },

  mounted() {
    setInterval(() => {
      this.setDateTime();
    }, 1000);
    //getUTChour
    setInterval(() => {
      this.setServerDate();
    },1000);
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