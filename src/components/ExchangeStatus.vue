<template>
  <div>
    <div @click="toggleDialog">
      <h1 class="h1"><exch-bar :exch="exch" :exchlist="exchlist" /></h1>
    </div>
    <window
      v-if="visible"
      :initial-width="600"
      :initial-height="200"
      :title="'Stock Exchange Time'"
      :resizable="true"
      @close="toggleDialog"
      :style="{ height: '150px', cursor: 'default' }"
    >
      <grid
        ref="grid"
        :style="{ height: '150px', cursor: 'pointer' }"
        :data-items="exchlist"
        :selected-field="selectedField"
        :columns="columns"
        :resizable="true"
        @rowclick="onRowClick"
        
      ></grid>
    </window>
  {{exch}}
  </div></template>
<script>
import { Grid } from "@progress/kendo-vue-grid";
import { Window } from "@progress/kendo-vue-dialogs";
import ExchBar from "./ExchBar.vue";

import "@progress/kendo-theme-default/dist/all.css";
export default {
  components: {
    Grid: Grid,
    window: Window,
    ExchBar,
  },
  props: ["exchlist"],
  data() {
    return {
      visible: false,
      glow: "white",
      simpleTime: true,
      selectedID: 1,
      exc: this.exchlist,
      exch: ["MYX"],
      selectedField: "selected",
      exchange: this.exchlist,
      staticColumns: [
        {
          field: "id",
          title: "ID",
          width: "60px",
        },
        {
          field: "name",
          title: "Exchange Name",
          width: "150px",
        },
        {
          field: "serverDate",
          title: "Time",
          width: "250px",
        
        },
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
      this.exch = [];
      this.exch.push(event.dataItem.id);
    },
    toggleDialog() {
      this.visible = !this.visible;
    },
  },
};
</script>
<style>
.h1 {
  transition: 0.2s;
  font-size: 10vh;
  font-family: monospace;
  margin: 1px;
  padding: 0px;
}
.no-cursor {
 cursor: default;
}
</style>
