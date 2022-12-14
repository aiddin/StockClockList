<template>
  <div>
    <window v-if="visible" :initial-width="600" :initial-height="200" :title="'Stock Exchange Time'" :resizable=true @close="toggleDialog" :color=blue>
     <div>
      <table class="table-auto bg-gray-900 table " v-for="exchlist in exchlist" :key="exchlist.id">
        <tr >
          <td class="text-white auto bg-gray-900 table" >
            <h1 class="huh">{{ exchlist.id }}</h1> 
          </td>
          <td  bg-gray-900 table>
            <h1 class="huh">{{exchlist.status}}</h1>
          </td>
          <td >
           {{exchlist.serverDate}}
          </td>
        </tr>
      </table>
    </div>
      <grid
        ref="grid"
        :style="{ height: '150px' }"
        :data-items="exchlist"
        :selected-field="selectedField"
        :columns="columns"
        :resizable="true"
        @rowclick="onRowClick"
      ></grid>
    </window>
    <div @click="toggleDialog">
      <tc-stock-exch :exch="exch" :exchlist="exchlist" />
    </div>
  </div>
</template>
<script>
import {Grid} from "@progress/kendo-vue-grid";
import {Window} from "@progress/kendo-vue-dialogs";
import TcStockExch from "./TcStockExch.vue";
import "@progress/kendo-theme-default/dist/all.css";
export default {
  components: {
    Grid: Grid,
    TcStockExch,
    'window': Window,
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
        { field: "id", title: "ID", width: "60px" },
        { field: "name", title: "Exchange Name", width: "150px" },
        { field: "status", title: "Status", width: "70px" },
        { field: "serverDate", title: "Time", width: "250px" },
      ],
    };
  },
  computed: {
    columns() {
      return [...this.staticColumns];
    },
  },
  // watch: {
  //   exch: {
  //     handler() {
  //       this.exchange = this.exchlist;
  //     },
  //     deep: true,
  //   },
  // },
  methods: {
    onRowClick(event) {
      event.dataItem[this.selectedField] = !event.dataItem[this.selectedField];
      this.exch = [];
      this.exch.push(event.dataItem.id);
    },
    toggleDialog() {
      this.visible = !this.visible;
    },
  },
};
</script>
