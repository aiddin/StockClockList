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
        { id: "MYX", name: "Malaysia Exchange ", status: "0", gmTime: "+8" },
        { id: "IDX", name: "Indonesia Exchange ", status: "1", gmTime: "+7" },
        { id: "HKEX", name: "Hong Kong Exchange ", status: "2", gmTime: "+8" },
        { id: "SGX", name: "Singapore Exchange ", status: "0", gmTime: "+8" }, // 1 hour == 3,600,000 milliseconds
      ],
    };
  },
};
</script>
