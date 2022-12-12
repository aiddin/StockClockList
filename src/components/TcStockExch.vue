<template>
  <div>
  <Grid
    ref="grid"

    :style="{ height: '150px' }"
    :data-items="exchange"
    :selected-field="selectedField"
    :columns="columns"
    @rowclick="onRowClick"
  ></Grid>
</div>
  <div>
    <table class="bg-gray-900 table w-full ">
        <tr
          class="border ..."
          v-for="exch in exch"
          :key="exch.id"
        >
          <td  class="border border-slate-700 ...">
            <tc-stock-stat :stat="exch.status" />
          </td>
          <td class="text-white border border-slate-700 ..." >
            {{ exch.id }}
          </td>
          <td class="text-white border border-slate-700 ...">
            {{ exch.name }}
          </td>
          <td class="text-white border border-slate-700 ...">
            <tc-clock 
           
            :serverDate="exch.serverDate1"
            :simpleTime="simpleTime"
            :glow="glow"
             > 
          </tc-clock>
          </td>
        </tr>
      
    </table>

  </div>
  {{exchange}}
  <!-- {{exchlist}}
  {{exchange}} -->
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

      // exc: this.exchange
      glow: 'white  ',
      simpleTime: true, 
      exc:this.exchlist,
      exch: [],
      huh: {},
      selectedField: "selected",
      exchange: this.exchlist,
      staticColumns: [
        { field: "id", title: "ID", width: "150px" },
        { field: "name", title: "Exchange Name" },
        { field: "status", title: "Status" },
        
      ],
    };
  },
   watch: {
  exchlist:{
    handler(){
      this.refreshArraydata();
    },
    deep: true
  },
  },

  computed: {
    columns() {
      return [...this.staticColumns];
    },
    matchingIds() {
      return this.exch.filter(obj1 =>
        this.exchange.some(obj2 => obj1.id === obj2.id)
      );
    },
    newObject() {
      var obj = {};
      obj = Object.assign({}, ...this.matchingIds());
      return  obj;
    }
  },
//     watch: {
// //     test() {
// //     // const obj;
// //     for (let key in this.exc) {
// //   if (this.exchlist.Object.prototype.hasOwnProperty.call(key)) {
// //     // If the property is not present in object2, delete it from object1
// //     this.huh.push(this.exc.dataItem)
// // }
// // }
// //   },
//      },
  methods: {
     refreshArraydata(){
      this.exchange= []
      this.exchange = this.exchlist;
     },
    setDateTime() {
      this.simpleTime = true;
    },

    onRowClick(event) {
      event.dataItem[this.selectedField] = !event.dataItem[this.selectedField];
      if (event.dataItem[this.selectedField] == false) {
        this.exch.splice(this.exch.indexOf(event.dataItem), 1);
      } else 
      {
        this.exch.push(event.dataItem);
        
      
      }
    },
  },
  mounted() {
 
 setInterval(() => {
   
   this.setDateTime();
 }, 1000);

},
 
 
 
};
</script>
