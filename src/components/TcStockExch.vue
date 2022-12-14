<template>
  <div>
    <table class="table-fixed bg-gray-900 table " v-for="exchlist in exchlist" :key="exchlist.id">
      
      <tr  v-if="filter(exchlist)" >
        <th   class="text-white auto" >
          <h1 class="huh">{{ exchlist.id }}</h1> 
        </th>
        <td>
          <h1 class="huh"> <status-view :stat="exchlist.status" /></h1>
        </td>
        <td >
          <h1 class="huh" ><tc-clock :serverDate="exchlist.serverDate" :simpleTime="simpleTime" :glow="glow">
          </tc-clock></h1>
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
<style scoped>
.huh{
  transition: 0.2s;
  font-size: 10vh ;
  font-family: monospace;
  margin: 1px;
  padding: 0px;
}
tr{
  cursor: pointer;
}
</style>
