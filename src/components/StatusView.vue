<template>
  <div :style="status" :stat="status">
    {{ status.message }}
  </div>
</template>
<script>
export default {
  props: ["stat"],
  data() {
    return {
      status: {
        message: "not found",
        color: "white",
      },
    };
  },
  watch: {
    stat: {
      handler() {
        this.test();
      },
      deep: true,
    },
  },
  created() {
    this.test();
  },
  methods: {
    test() {
      if (this.stat == 0) {
        this.status = {
          message: "OPEN",
          color: "greenyellow",
        };
      } else if (this.stat == 1) {
        this.status = {
          message: "CLOSE",
          color: "red",
        };
      } else if (this.stat == 2) {
        this.status = {
          message: "BREAK",
          color: "orange",
        };
      }
    },
  },
};
</script>

