
//choosen stock list from tcstockexch
<template>


    <div>

      <table  v-on:mouseover="active = !active" class="bg-gray-900 table w-full ">
        
          <tr
            class="border ..."
            v-for="exc in exc"
            :key="exc.id" 
          >
            <td  class="border border-slate-700 ...">
              <tc-stock-stat :stat="exc.status" />
            </td>
            <td class="text-white border border-slate-700 ..." >
              {{ exc.id }}
            </td>
            <td class="text-white border border-slate-700 ...">
              {{ exc.name }}
            </td>
            <td class="text-white border border-slate-700 ...">
              <tc-clock 
             
              :serverDate="exc.serverDate1"
              :simpleTime="simpleTime"
               > 
            </tc-clock>
            </td>
          </tr>
        
      </table>
      {{exc}}
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
      active: true,
      exc: this.exch,
     
      simpleTime: true, 
    };
  },
  computed: {
   
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
    }, 0);
   
  },
};
</script>
