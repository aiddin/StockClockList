<template>

  
    <div>
      <table v-on:mouseover="active = !active" class="border-slate-400 w-fill">
        <tbody>
          <tr
            class="border-collapse border border-slate-400"
            v-for="exch in exch"
            :key="exch.id"
          >
            <td :style="styleTest" class="tdstyle">
              <tc-stock-stat :stat="exch.status" />
            </td>
            <td class="tdstyle">
              {{ exch.id }}
            </td>
            <td class="tdstyle">
              {{ exch.name }}
            </td>
            <td>
              <tc-clock :serverDate="serverDate" :simpleTime="simpleTime"> </tc-clock>
            </td>
          </tr>
        </tbody>
      </table>
    </div>

</template>

<script>
import TcClock from "../components/TcClock.vue";
import TcStockStat from "../components/TcStockStat.vue";

import "@progress/kendo-theme-default/dist/all.css";
const date = new Date();
export default {
  components: {
    TcClock,
    TcStockStat,
  
  },

  props: ["exch"],
  data() {
    return {
      active: false,

      visible: true,
      serverDate: date,
      simpleTime: true,
      statColor: this.exch.status,
    };
  },

  computed: {
    styleTest() {
      if (this.statColor === "0") {
        return {
          color: "green",
        };
      } else if (this.statColor === "1") {
        return {
          color: "red",
        };
      } else if (this.statColor === "2") {
        return {
          color: "yellow",
        };
      } else {
        return {
          color: "blue",
        };
      }
    },
  },
  methods: {
    setDateTime() {
      this.glow = "";
      this.simpleDate = true;
      this.simpleTime = true;
      this.simpleDateTime = true;
      this.advancedTime = true;
    },
    setServerDate() {
      const date1 = new Date();
      

      // date1.setMilliseconds((Math.floor((Math.random()* 4)+2))*1000); test random second diff
     
      this.serverDate = date1;
    },
  },

  mounted() {
    setInterval(() => {
      this.setDateTime();
    }, 1000);
    //getUTChour
    setInterval(() => {
      this.setServerDate();
    }, 1000);
  },
};
</script>
<style>
th {
  padding-right: 15px;
  padding-left: 15px;
  padding-bottom: 15px;
}
table{
    background-color: #2b2b2b;
    scroll-snap-type: both mandatory;
    width: auto;
}
.tdstyle {
  color: #fff;
  scroll-snap-align: start;
  font-weight: 500;
  margin: 150vw;
  padding: 50px;
  font-size: 5vh;
  font-family: Oxygen, monospace;
}
.huh {
  margin: 0 auto;
  padding: 50px;
}
</style>
