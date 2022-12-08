
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
      serveDate: this.datetrhin(),
  
      exchlist: [
        { id: "MYX", name: "Malaysia Exchange ", status: "0", GMT: +8, serverDate: this.serveDate, },
        { id: "IDX", name: "Indonesia Exchange ", status: "2", GMT: +7 ,serverDate: this.datetrhin(),},
        { id: "TSX", name: "Toronto Stock Exchange", status: "1", GMT: -5 ,serverDate: date,},
        { id: "SGX", name: "Singapore Exchange ", status: "0", GMT: +8 ,serverDate: date,},
        { id: "KRX", name: "Korean Exchange", status: "0", GMT: +9 ,serverDate: date, },
        { id: "TWSE", name: "Taiwan Stock Exchange ", status: "0", GMT: +8 ,serverDate: date, },
        { id: "XAMS", name: "Euronext Amsterdam ", status: "0", GMT: +1 ,serverDate: date,}, // 1 hour == 3,600,000 milliseconds
      ],
    };
  },
  methods: {
    datetrhin() {
      const date1 = new Date();
      return date1;
    },
    
  },

    mounted() {
      setInterval(() => {
        this.datetrhin();
        
        
      }, 1000);
    },
  
};
</script>
