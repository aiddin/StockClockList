<template>
  <exchange-status :exchlist="exchlist"></exchange-status>
</template>
<script>
const date = new Date();
import ExchangeStatus from "./components/ExchangeStatus.vue";
export default {
  name: "App",
  components: {
    ExchangeStatus,
  },
  data() {
    return {
      exchlist: [
        { id: "MYX", name: "Malaysia Exchange ", status: "0", serverDate: date },
        { id: "IDX", name: "Indonesia Exchange ", status: "2", serverDate: date },
        { id: "TSX", name: "Toronto Stock Exchange", status: "1", serverDate: date },
        { id: "SGX", name: "Singapore Exchange ", status: "2", serverDate: date },
        { id: "KRX", name: "Korean Exchange", status: "0", serverDate: date },
        { id: "TWSE", name: "Taiwan Stock Exchange ", status: "2", serverDate: date },
        { id: "XAMS", name: "Euronext Amsterdam ", status: "1", serverDate: date },
      ],
    };
  },
  methods: {
    //randomize status and time
    setServerDate() {
      const date1 = new Date();
      date1.setMilliseconds(Math.floor(Math.random() * 8 + 2) * 1000);
      const date2 = new Date();
      date2.setMilliseconds(Math.floor(Math.random() * 8 + 2) * 1000);
      const date3 = new Date();
      date3.setMilliseconds(Math.floor(Math.random() * 8 + 2) * 1000);
      var stattest = Math.floor(Math.random() * 3 + 0);
      var stattest1 = Math.floor(Math.random() * 3 + 0);
      var stattest2 = Math.floor(Math.random() * 3 + 0);
      this.serverDate = date1;
      this.exchlist = [
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
          serverDate: date2,
        },
        {
          id: "TSX",
          name: "Toronto Stock Exchange",
          status: stattest2,
          serverDate: date3,
        },
        { id: "SGX", name: "Singapore Exchange ", status: "2", serverDate: date1 },
        { id: "KRX", name: "Korean Exchange", status: "0", serverDate: date2 },
        {
          id: "TWSE",
          name: "Taiwan Stock Exchange ",
          status: "2",
          serverDate: date3,
        },
        {
          id: "XAMS",
          name: "Euronext Amsterdam ",
          status: "1",
          serverDate: date1,
        },
      ];
    },
  },
  mounted() {
    setInterval(() => {
      this.setServerDate();
    }, 1000);
  },
};
</script>
