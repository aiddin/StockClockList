
//choosen stock list from tcstockexch
<template>


    <div>
      <table  v-on:mouseover="active = !active" class="bg-gray-900 table w-full ">
        {{exc}}{{exch}}
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
              v-for="(serverDate,exc) in exc.length"
              :key="exc.id"
              :serverDate="exc.map(a => serverDate.serverDate)"
              :simpleTime="simpleTime"
               > 
            </tc-clock>
            </td>
          </tr>
        
      </table>
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

  props: ["exch"],
  data() {
    return {
      active: false,
      exc: this.exch,

      serverDate: this.exch.serverDate,
      simpleTime: true,
    };
  },
  computed: {
   
  },
  methods: {
    setDateTime() {
      this.simpleTime = true;
       
      this.serverDate = this.exc.serverDate;
   
    },
   
  },
  // beforeMount(){
  //   this.setServerDate();
  // },
  mounted() {
    setInterval(() => {
      console.log(this.serverDate);
      this.setDateTime();
    }, 1000);
   
  },
};
</script>
