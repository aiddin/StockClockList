
<template>
  <tc-stock-exch :exchlist="exchlist"></tc-stock-exch>
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
      exchlist: [
        { id: "MYX", name: "Malaysia Exchange ", status: "0", serverDate: date, },
        { id: "IDX", name: "Indonesia Exchange ", status: "2",serverDate: date},
        { id: "TSX", name: "Toronto Stock Exchange", status: "1" ,serverDate: date,},
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
      date1.setMilliseconds((Math.floor((Math.random()* 8)+2))*1000);
      var stattest = Math.floor((Math.random()* 2)+0);
      var stattest1 = Math.floor((Math.random()* 2)+0);
      var stattest2 = Math.floor((Math.random()* 2)+0);
      this.serverDate = date1;
      this.exchlist=[
        {
          id: "MYX",
          name: "Malaysia Exchange ",
          status: stattest,
          serverDate: date1,

        },
        {
          id: "IDX",
          name: "Indonesia Exchange ",
          status: stattest1,
          serverDate: date1,
        },
        {
          id: "TSX",
          name: "Toronto Stock Exchange",
          status: stattest2,
          serverDate: date1,
        }
      ]
    },
  },
    mounted() {
      setInterval(() => {
        this.setServerDate();
      }, 2000);
    },
  
};
</script>
