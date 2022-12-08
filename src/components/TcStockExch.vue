<template>
  <Grid
    ref="grid"
    :style="{ height: '300px' }"
    :data-items="exchange"
    :selected-field="selectedField"
    :columns="columns"
   
    @rowclick="onRowClick"
  >
    <tc-stock-stat :stat="exch.status" />
  </Grid>

  <tc-stock-list :exch="exch"></tc-stock-list>
</template>

<script>
import { Grid } from "@progress/kendo-vue-grid";
import "@progress/kendo-theme-default/dist/all.css";
import TcStockList from "./TcStockList.vue";
import TcStockStat from "./TcStockStat.vue";
export default {
  components: {
    TcStockList,
    TcStockStat,
    Grid: Grid,
  },
  props: ["exchlist"],
  data() {
    return {
      exch: [],
      selectedField: "selected",
      exchange: this.exchlist,

      staticColumns: [
        { field: "id", title: "ID", width: "150px" },
        { field: "name", title: "Exchange Name" },
        { field: "status", title: "Status" },
      ],
    };
  },
  computed: {
    columns() {
      return [...this.staticColumns];
    },
  },
  methods: {
    onRowClick(event) {
      event.dataItem[this.selectedField] = !event.dataItem[this.selectedField];
      if (event.dataItem[this.selectedField] == false) {
        this.exch.splice(this.exch.indexOf(event.dataItem), 1);
      } else this.exch.push(event.dataItem);
      console.log(this.exch);
    },
  },
};
</script>
