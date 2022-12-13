
<template>
  <window><exchange-status :exchlist="exchlist"/></window>
  <div>
    <table class="table-fixed bg-gray-900 table " v-for="exchlist in exchlist" :key="exchlist.id">
      <tr  v-if="filter(exchlist)" >
        <td class="text-white auto" >
          <h1 class="huh">{{ exchlist.id }}</h1> 
        </td>
        <td>
          <h1 class="huh"><tc-stock-stat :stat="exchlist.status" /></h1>
        </td>
        <td >
         <tc-clock :serverDate="exchlist.serverDate" :simpleTime="simpleTime" :glow="glow">
          </tc-clock>
        </td>
      </tr>
    </table>
  </div>

 
</template>
<script>
import TcClock from "../components/TcClock.vue";
import TcStockStat from "../components/TcStockStat.vue";
import ExchangeStatus from "../components/ExchangeStatus.vue";
export default {
  components: {
    TcClock,
    TcStockStat,
    ExchangeStatus
    // Grid: Grid,
  },

  props: ["exchlist"],
  data() {
    return {
      glow: "white",
      simpleTime: true,
      selectedID: 1,
      exc: this.exchlist,
      exch: ['MYX'],
      selectedField: "selected",
      exchange: this.exchlist,
      
    };
  },
  methods: {
    filter(exchlist) {
        return this.exch.find(id => id === exchlist.id);
    },
    
  }, 
};
</script>
<style>

.huh{
  transition: 0.2s;
  font-size: 6vh;
  margin: 0;
  padding: 0;
}
</style>
