
<template>
  <tc-stock-exch  v-bind:exchlist="exchlist"></tc-stock-exch>
</template>
<script>
      const date = new Date();
import TcStockExch from "./components/TcStockExch.vue";
export default {
  name: "App",
  components: {
    TcStockExch,
   
  },
  data() {
    return {
      serveDate1: date,
      
      exchlist: [
        { id: "MYX", name: "Malaysia Exchange ", status: "0", GMT: +8, serverDate1: this.serveDate, },
        { id: "IDX", name: "Indonesia Exchange ", status: "2", GMT: +7 ,serverDate1: date},
        { id: "TSX", name: "Toronto Stock Exchange", status: "1", GMT: -5 ,serverDate1: date,}
        // { id: "SGX", name: "Singapore Exchange ", status: "0", GMT: +8 ,serverDate: date,},
        // { id: "KRX", name: "Korean Exchange", status: "0", GMT: +9 ,serverDate: date, },
        // { id: "TWSE", name: "Taiwan Stock Exchange ", status: "0", GMT: +8 ,serverDate: date, },
        // { id: "XAMS", name: "Euronext Amsterdam ", status: "0", GMT: +1 ,serverDate: date,}, // 1 hour == 3,600,000 milliseconds
      ],
    };
  },
  methods: {
  setServerDate() {
      const date1 = new Date();
      date1.setMilliseconds((Math.floor((Math.random()* 4)+2))*1000);
      this.exchlist=[
        {
          id: "MYX",
          name: "Malaysia Exchange ",
          status: "0",
          GMT: +8,
          serverDate1: this.serveDate,

        },
        {
          id: "IDX",
          name: "Indonesia Exchange ",
          status: "2",
          GMT: +7,
          serverDate1: date1,
        },
        {
          id: "TSX",
          name: "Toronto Stock Exchange",
          status: "1",
          GMT: -5,
          serverDate1: date1,
        }
      ]
      // 
     console.log(date1)

    },
  },
    mounted() {
      setInterval(() => {
        this.setServerDate();
        
        
      }, 1000);
    },
  
};
</script>
