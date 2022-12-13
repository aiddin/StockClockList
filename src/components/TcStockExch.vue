<template>
  <div>
    <grid
      ref="grid"
      :style="{ height: '150px' }"
      :data-items="exchlist"
      :selected-field="selectedField"
      :columns="columns"
      :resizable="true"
      @rowclick="onRowClick"
    ></grid>
  </div>
  <div>
    <table class="table-fixed bg-gray-900 table w-full" v-for="exchlist in exchlist" :key="exchlist.id">
      <tr  v-if="filter(exchlist)" >
       
        <td class="text-white auto" >
          {{ exchlist.id }}
        </td>
        <td>
          <h1 class="" > <tc-stock-stat :stat="exchlist.status" /></h1>
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
import { Grid } from "@progress/kendo-vue-grid";
import "@progress/kendo-theme-default/dist/all.css";

export default {
  components: {
    TcClock,
    TcStockStat,
    Grid: Grid,
  },

  props: ["exchlist"],
  data() {
    return {
      glow: "yellow",
      simpleTime: true,
      selectedID: 1,
      exc: this.exchlist,
      exch: [],
      selectedField: "selected",
      exchange: this.exchlist,
      staticColumns: [
        { field: "id", title: "ID", width: "150px" },
        { field: "name", title: "Exchange Name" },
        { field: "status", title: "Exchange Status" },
        { field: "serverDate", title: "Exchange Time" },
      ],
    };
  },
  computed: {
    columns() {
      return [...this.staticColumns];
    },
  },
  methods: {
    filter(exchlist) {
        return this.exch.find(id => id === exchlist.id);
    },
    onRowClick(event) {
      event.dataItem[this.selectedField] = !event.dataItem[this.selectedField];
      this.exch =[];
      this.exch.push(event.dataItem.id);
    },
  },
  
};
</script>
