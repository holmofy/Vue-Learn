<template>
  <div v-on:click="toggle" v-bind:title="titleText">
      <span>当前时间为：</span>
      <span>{{nowTimeString}}</span>
  </div>
</template>

<script>
export default {
  name: "TimeClock",
  data: () => ({
    time: new Date(),
    timerID: undefined
  }),
  computed: {
    nowTimeString: function() {
      return this.time.toLocaleTimeString();
    },
    titleText: function() {
      return this.timerID ? "点击暂停" : "点击继续";
    }
  },
  mounted: function() {
    this.start();
  },
  methods: {
    start: function() {
      this.timerID = setInterval(() => this.tick(), 1000);
    },
    stop: function() {
      this.timerID = clearInterval(this.timerID);
    },
    toggle: function() {
      this.timerID ? this.stop() : this.start();
    },
    tick: function() {
      this.time = new Date();
    }
  }
};
</script>
