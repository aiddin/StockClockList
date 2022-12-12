
//choosen stock list from tcstockexch
<template>


    <div>

      <table class="bg-gray-900 table w-full ">
        
          <tr
            class="border ..."
            v-for="huh in huh"
            :key="huh.id" 
          >
            <td  class="border border-slate-700 ...">
              <tc-stock-stat :stat="huh.status" />
            </td>
            <td class="text-white border border-slate-700 ..." >
              {{ huh.id }}
            </td>
            <td class="text-white border border-slate-700 ...">
              {{ huh.name }}
            </td>
            <td class="text-white border border-slate-700 ...">
              <tc-clock 
             
              :serverDate="huh.serverDate1"
              :simpleTime="simpleTime"
              :glow="glow"
               > 
            </tc-clock>
            </td>
          </tr>
        
      </table>
      {{huh}}
    </div>

</template>

<script>
import TcClock from "../components/TcClock.vue";
import TcStockStat from "../components/TcStockStat.vue";

import "@progress/kendo-theme-default/dist/all.css";

export default {
  components: {
    TcClock,
    TcStockStat,
  
  },

  props: ["exch","exchange"],
  data() {
    return {
      active: true,
      exc: this.exch,
      // exc: this.exchange,
      huh:[],
      exchlist: this.exchange,
      glow: 'white  ',
      simpleTime: true, 
    };
  },
  watch: {
   test() {
    // const obj;
    for (let key in this.exc) {
  if (this.exchlist.Object.prototype.hasOwnProperty.call(key)) {
    // If the property is not present in object2, delete it from object1
    this.huh.push(this.exc.dataItem)
}
}

  },
},

  methods: {
    setDateTime() {
      this.simpleTime = true;
      this.exc=this.exch;
     
    },
   
  },
  // beforeMount(){
  //   this.setServerDate();
  // },
  mounted() {
 
    setInterval(() => {
      
      this.setDateTime();
    }, 1000);
   
  },
};
</script>
