<!-- :simpleDate="simpleDate"
:simpleTime="simpleTime"
:simpleDateTime="simpleDateTime" -->
<template>
  <tc-stock-exch :exchlist="exchlist"></tc-stock-exch>
</template>
<script>

import TcStockExch from "./components/TcStockExch.vue";
export default {
  name: "App",
  components: {
    TcStockExch,
   
  },
  data() {
    return {
      exchlist: [
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
