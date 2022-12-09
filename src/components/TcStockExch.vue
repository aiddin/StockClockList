<template>
  <Grid
    ref="grid"

    :style="{ height: '300px' }"
    :data-items="exchange"
    :selected-field="selectedField"
    :columns="columns"
    @rowclick="onRowClick"
  ></Grid>

  <tc-stock-list :exch="exch"></tc-stock-list>
</template>

<script>
import { Grid } from "@progress/kendo-vue-grid";
import "@progress/kendo-theme-default/dist/all.css";
import TcStockList from "./TcStockList.vue";
export default {
  components: {
    TcStockList,
    
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
        { field: "serverDate1", title: "Server Date" },
      ],
    };
  },
  //  watch: {
  // serverDate1: function () {
  //   this.exchange = this.exchlist;

  // },
  // },
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
      
    },
  },
  mounted() {
    setInterval(() => {
      this.exchange = this.exchlist;
    }, 0);
  

  },
 
 
};
</script>
