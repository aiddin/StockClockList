<template><div class="stockbg">
  <table class="huh">
    <tbody>
    <tr v-for="exch in exch" :key="exch.id">
        <td class="tdstyle">
            <tc-stock-stat :stat="exch.status" />
          </td>
        <td class="tdstyle">
            {{ exch.id }}
        </td>
      <td class="tdstyle">
        {{ exch.name }}
      </td>
      <td>
        <tc-clock :serverDate="serverDate" :glow="glow" :simpleTime="simpleTime">
        </tc-clock>
      </td>
    </tr>
</tbody>
  </table>
</div>
</template>

<script>
import TcClock from "../components/TcClock.vue";
import TcStockStat from "../components/TcStockStat.vue";
const date = new Date();
export default {
  components: {
    TcClock,
    TcStockStat,
  },
  
  props: ["exch"],
  data(){
    return{

      serverDate: date,
      simpleTime: true,
     
    }
  },
  methods: {
    setDateTime() {
      this.glow = '';
      this.simpleDate = true;
      this.simpleTime = true;
      this.simpleDateTime = true;
      this.advancedTime = true;
      
    },
    setServerDate() {
      const date = new Date();
      
      console.log (-date.getTimezoneOffset()/60+'heh')//get utc time offset
     date.setHours(date.getHours() + (-1) );
      this.serverDate = date;
    },
  },

  mounted() {
    setInterval(() => {
      this.setDateTime();
    }, 1000);
    //getUTChour
    setInterval(() => {
      this.setServerDate();
    },1000);
  },
  }
;
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->

<style>
th {
  padding-right: 15px;
  padding-left: 15px;
  padding-bottom: 15px;
}

.stockbg{
  background-color: #2b2b2b;
  
}
.tdstyle{
  
  color: #fff;
  
  font-weight: 500;
  margin : 150vw;
  padding: 50px;
  font-size :5vh;
  font-family: Oxygen, monospace;
}
.huh{
  margin: 0 auto;
  padding: 50px;
}

</style>
