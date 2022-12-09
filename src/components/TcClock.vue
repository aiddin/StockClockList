<template>
  <div id="clock">
    <h1 :style="style">{{ advancedDateSet }}</h1>
    <h2 :style="style">
      {{ simpleDateTimeSet }}{{ simpleDateSet }}{{ simpleTimeSet }}{{ advancedTimeSet }}
    </h2>
  </div>
</template>

<script>

import { defineComponent } from "vue";
//TODO : add a prop to change the time zone 
//USE TIME DIFFER ADD TO LOCAL TIME PROP
//DETACH SERVER DATE & TIME FROM LOCAL DATE & TIME
export default defineComponent({
  //props from TcData component
  props: [
    "serverDate",
    "glow",
    "GMT",
    "simpleTime",
    "simpleDate",
    "simpleDateTime",
    "advancedTime",
  ],
  name: "TcClock",

  data() {
    return {
      timeDiff: this.timeDiffer(),
      localDate: this.clientTime(),

      advancedTimeBool: this.advancedTime,
      advancedDateBool: this.advancedTime,

      simpleTimeSet: this.setSimpleTime(),
      simpleDateSet: this.setSimpleDate(),
      simpleDateTimeSet: this.setSimpleDateTime(),
      advancedTimeSet: this.setAdvancedTime(),
      advancedDateSet: this.setAdvancedDate(),

      dateServer: this.serverDate,
    };
  },

  methods: {
    //setting date time format
    setSimpleDateTime() {
      if (this.simpleDateTime !== undefined) {
        var set = Intl.DateTimeFormat("en-GB", {
          weekday: "short",
          day: "2-digit",
          month: "short",
          hour: "2-digit",
          minute: "2-digit",
        }).format(this.localDate);
        return set;
      } else return "";
    },
    setSimpleDate() {
      if (this.simpleDate !== undefined) {
        var set = Intl.DateTimeFormat("en-GB", {
          weekday: "short",
          day: "2-digit",
          month: "short",
          year: "numeric",
        }).format(this.localDate);
        return set;
      } else return (set = "");
    },
    setSimpleTime() {
      if (this.simpleTime !== undefined) {
        const set = Intl.DateTimeFormat("en-US", {
          hour: "2-digit",
          minute: "2-digit",
          second: "numeric",
        }).format(this.localDate);
        return set;
      } else return "";
    },
    setAdvancedDate() {
      if (this.advancedTimeBool !== undefined) {
        var set = Intl.DateTimeFormat("en-MY", {
          year: "numeric",
          day: "2-digit",
          month: "short",
          weekday: "short",
        }).format(this.localDate);
        return set;
      } else return (set = "");
    },
    setAdvancedTime() {
      if (this.advancedTimeBool !== undefined) {
        var set = Intl.DateTimeFormat("en-US", {
          hour: "2-digit",
          minute: "2-digit",
          second: "2-digit",
        }).format(this.localDate);
        return set;
      } else return (set = "");
    },

    //setting client time and date
    clientTime() {
      const dateLocal1 = new Date();
      dateLocal1.setMilliseconds(parseInt(this.timeDiff));
      return dateLocal1;
    },
    //setting time difference
    timeDiffer() {                                             
      const dateLocal12 = new Date();
      
      const dateServer1= new Date(Date.parse(this.serverDate));
      // const dateServer1 = new Date.parse(this.serverDate);
      const timeDiff = dateServer1.getTime()- dateLocal12.getTime();
      
      return timeDiff;
    },
    //set date time for set interval
    setDateTime() {
      this.localDate = this.clientTime();
      this.simpleDateTimeSet = this.setSimpleDateTime();
      this.simpleDateSet = this.setSimpleDate();
      this.simpleTimeSet = this.setSimpleTime();
      this.advancedTimeSet = this.setAdvancedTime();
      this.advancedDateSet = this.setAdvancedDate();
    },
  },

  computed: {
    //styling for glow fx
    style() {
      if (this.glow == undefined) return "";
      else
        return {
          "text-shadow": "0 0 20px rgb(39, 83, 149), 0 0 20px rgba(10, 175, 230, 0)",
          color: this.glow,
        };
    },
  },
  watch: {
  serverDate: function (newVal) {
    this.dateServer = newVal;
    this.timeDiff= null;
    this.localDate=null;
    this.timeDiff = this.timeDiffer();
    this.localDate= this.clientTime();
    
  },
  },
beforeMount() {

      this.timeDiffer(), this.clientTime();
  },
  mounted() {
    setInterval(() => {

      this.setDateTime();
    }, 0);
  },
  beforeUnmount() {
    clearInterval(this.setDateTime);
  },
});
</script>
<style>
#clock {
  height: stretch;
  width: stretch;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  position: sticky;
  left: 0;
  top: 0;
  color: greenyellow;
  transition: 0.2s;
  text-align: justify;
  font-family: monospace;
  background-color: rgba(34, 34, 34, 0);
}
#clock h1 {
  transition: 0.2s;
  font-size: 5vh;
  margin: 0;
  padding: 0;
}
#clock h2 {
  transition: 0.2s;
  font-size: 8vh;
  margin: 0;
  padding: 0;
}
</style>
