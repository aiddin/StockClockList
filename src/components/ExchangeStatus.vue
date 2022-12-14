<template>
  <div>
    <window v-if="visible" :initial-width="600" :initial-height="200" :title="'Stock Exchange Time'" :resizable=true @close="toggleDialog" :color=blue>
     <div >
      <table class="table-auto bg-gray-900 table " >
        <tr>
          <th><h1>id</h1></th>
          <th><h1>status</h1></th>
          <th><h1>time</h1></th>
        </tr>
        <tr class="trhover" v-for="exchlist in exchlist" :key="exchlist.id"  @click="test(exchlist, $event)">
          <td class="text-white auto bg-gray-900 " >
            <h1 class="id">{{ exchlist.id }}</h1> 
          </td>
          <td  class="text-white auto bg-gray-900 ">
            <h1 class="status"><status-view :stat="exchlist.status"/></h1>
          </td>
          <td class="text-white auto bg-gray-900 ">
          <h1 class="">{{exchlist.serverDate}}</h1> 
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
  {{exch}}
</template>
<script>
import {Grid} from "@progress/kendo-vue-grid";
import {Window} from "@progress/kendo-vue-dialogs";
import TcStockExch from "./TcStockExch.vue";
import StatusView from "./StatusView.vue";
import "@progress/kendo-theme-default/dist/all.css";
export default {
  components: {
    Grid: Grid,
    TcStockExch,
    StatusView,
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
      
      this.exch = [];
      this.exch.push(event.dataItem.id);
    },
    test(exchlist, event) {
      this.exch = [];
      this.exch.push(event.exchlist);
      console.log(exchlist)
    },
    toggleDialog() {
      this.visible = !this.visible;
    },
  },
};
</script>
<style >
.huh{
  transition: 0.2s;
  font-size: 10vh ;
  font-family: monospace;
  margin: 1px;
  padding: 0px;
}
.trhover{
  cursor: pointer;
  background-color: #ffff99;
}

</style>

