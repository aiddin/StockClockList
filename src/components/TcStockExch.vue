<template>
  <div>
    <table class="table-auto bg-gray-900 table " v-for="exchlist in exchlist" :key="exchlist.id">
      <tr  v-if="filter(exchlist)" >
        <td class="text-white auto" >
          <h1 class="huh">{{ exchlist.id }}</h1> 
        </td>
        <td>
          <h1 class="huh"><status-view :stat="exchlist.status" /></h1>
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
import StatusView from "./StatusView.vue";

export default {
  components: {
    TcClock,
   StatusView,

    // Grid: Grid,
  },

  props: ["exchlist", "exch"],
  data() {
    return {
      glow: "white",
      simpleTime: true,
      selectedID: 1,
      exc: this.exch,
      selectedField: "selected",      
    };
  },
  watch: {
    exch:{
    handler(){
      this.exc = this.exch;
    },
    deep:true,
  },
  },
  methods: {
    filter(exchlist) {
        return this.exc.find(id => id === exchlist.id);
    },
  }, 
};
</script>
<style>
.huh{
  transition: 0.2s;
  font-size: 6vh;
  margin: 5;
  padding: 5;
}
</style>
