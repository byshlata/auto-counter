<template>
  <div id="container">

    <div>{{ hour ? hour : '' }}</div>

    <div>{{ minute ? minute : '' }}</div>

    <div>{{ second }}</div>
  </div>
  <div id="container">

    <button @click="start">Start</button>

    <button @click="pause">Pause</button>

    <button @click="reset">Stop</button>
  </div>

</template>

<script lang="ts">
import { defineComponent } from 'vue';
import Counter from './utils/Counter';

export default defineComponent({

  data() {
    return {
      second: 0,
      minute: 0,
      hour: 0,
      isPause: false,
      Counter: new Counter(),
    };
  },
  methods: {
    changeTime(second: number, minute: number, hour: number): void {
      this.second = second;
      this.minute = minute;
      this.hour = hour;
    },

    start(): void {
      this.Counter.subscribe(this.changeTime);
      this.Counter.start();
    },

    reset(): void {
      this.Counter.reset();
    },

    pause(): void {
      this.Counter.pause();
    },
  },
});
</script>

<style>
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

</style>
