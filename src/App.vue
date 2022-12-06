<!-- :simpleDate="simpleDate"
:simpleTime="simpleTime"
:simpleDateTime="simpleDateTime" -->
<template>
  
  <tc-stock-list :exch="exch"></tc-stock-list>
</template>
<script>
import TcStockList from "./components/TcStockList.vue";
export default {
  name: "App",
  components: {
    TcStockList,
  },
  data() {
    return {
      exch: [
        { id: "MYX", name: "Malaysia Exchange ", status: "0", GMT: +8 },
        { id: "IDX", name: "Indonesia Exchange ", status: "2", GMT: +7 },
        { id: "TSX", name: "Toronto Stock Exchange", status: "1", GMT: -5 },
        { id: "SGX", name: "Singapore Exchange ", status: "0", GMT: +8 },
        { id: "KRX", name: "Korean Exchange", status: "0", GMT: +8 },
        { id: "TWSE", name: "Taiwan Stock Exchange ", status: "0", GMT: +8 },
        { id: "XAMS", name: "Euronext Amsterdam ", status: "0", GMT: +8 }, // 1 hour == 3,600,000 milliseconds
      ],
    };
  },
};
</script>
