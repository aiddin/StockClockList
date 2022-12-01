
<template>
  <div id="clock">
    <h1 :style="style">{{ advancedDateSet }}</h1>
    <h2 :style="style">
      {{ simpleDateTimeSet }}{{ simpleDateSet }}{{ simpleTimeSet }}{{ advancedTimeSet }}
    </h2>
  </div   >
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  //props from TcData component
  props: [
    "serverDate",

    "glow",


    "simpleTime",
    "simpleDate",
    "simpleDateTime",
    "advancedTime",
  ],
  name: "TcClock",

  data() {
    return {
      timeDiff: this.timeDiffer(),

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
        }).format(this.clientTime());
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
        }).format(this.clientTime());
        return set;
      } else return (set = "");
    },
    setSimpleTime() {
      if (this.simpleTime !== undefined) {
        const set = Intl.DateTimeFormat("en-US", {
          hour: "2-digit",
          minute: "2-digit",
          second: "numeric",
        }).format(this.clientTime());
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
        }).format(this.clientTime());
        return set;
      } else return (set = "");
    },
    setAdvancedTime() {
      if (this.advancedTimeBool !== undefined) {
        var set = Intl.DateTimeFormat("en-US", {
          hour: "2-digit",
          minute: "2-digit",
          second: "2-digit",
        }).format(this.clientTime());
        return set;
      } else return (set = "");
    },
   
    //setting client time and date
    clientTime() {
      const dateLocal1 = new Date();
      dateLocal1.setMilliseconds(parseInt(this.timeDiffer()));
      return dateLocal1;
    },
    //setting time difference
    timeDiffer() {
      const dateLocal1 = new Date();
      const dateServer1 = this.serverDate;
      const timeDiff = dateLocal1.getTime() - dateServer1.getTime();
      return timeDiff;
    },
    //set date time for set interval
    setDateTime() {
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
  color: rgb(243, 243, 243);
  transition: 0.2s;
  text-align: justify;
  font-family: "Oxygen", monospace;
  background-color: rgba(34, 34, 34, 0.801);
}
#clock h1 {
  transition: 0.2s;
  font-size: 5vw;
  margin: 0;
  padding: 0;
}
#clock h2 {
  transition: 0.2s;
  font-size: 8vw;
  margin: 0;
  padding: 0;
}
</style>
