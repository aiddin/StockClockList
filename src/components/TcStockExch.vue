<template>
  <div>
    <grid
      ref="grid"
      :style="{ height: '150px' }"
      :data-items="exchange"
      :selected-field="selectedField"
      :columns="columns"
      @rowclick="onRowClick"
    ></grid>
  </div>
  <div>
    <table class="bg-gray-900 table w-full" v-for="exchlist in exchlist" :key="exchlist.id">
      <tr class="border ..." v-if="filter(exchlist)" >
        <td class="border border-slate-700 ...">
          <tc-stock-stat :stat="exchlist.status" />
        </td>
        <td class="text-white border border-slate-700 ...">
          {{ exchlist.id }}
        </td>
        <td class="text-white border border-slate-700 ...">
          {{ exchlist.name }}
        </td>
        <td class="text-white border border-slate-700 ...">
          <tc-clock :serverDate="exchlist.serverDate" :simpleTime="simpleTime" :glow="glow">
          </tc-clock>
        </td>
      </tr>
    </table>
  </div>
  {{exchlist}}
  {{exch}}
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
      glow: "white",
      simpleTime: true,
      exc: this.exchlist,
      exch: [],

      selectedField: "selected",
      exchange: this.exchlist,
      staticColumns: [
        { field: "id", title: "ID", width: "150px" },
        { field: "name", title: "Exchange Name" },
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
      if (event.dataItem[this.selectedField] == false) {
        this.exch.splice(this.exch.indexOf(event.dataItem.id), 1);
      } else {
        this.exch.push(event.dataItem.id);
      }
    },
  },
  
};
</script>
