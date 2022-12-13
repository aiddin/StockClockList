<template>
  <div>
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
  </div>
</template>

<script>
import { Grid } from "@progress/kendo-vue-grid";

import "@progress/kendo-theme-default/dist/all.css";
export default {
  components: {
    Grid: Grid,
  },
  props: ["exchlist"],
  data() {
    return {
      glow: "white",
      simpleTime: true,
      selectedID: 1,
      exc: this.exchlist,
      exch: ["MYX"],
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
    onRowClick(event) {
      event.dataItem[this.selectedField] = !event.dataItem[this.selectedField];
      this.exch = [];
      this.exch.push(event.dataItem.id);
    },
  },
};
</script>
<style></style>
