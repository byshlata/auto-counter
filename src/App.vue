<template>
  <div class="app">
    <div class="pageContainer">
      <div v-for="key in counters" :key="key">
        <counter-time/>
      </div>

      <button class="btn" @click="addCounter">
        <div class="cross">
          <div class="line"/>
          <div class="line lineVer"/>
        </div>
      </button>
    </div>

  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import counterTime from '@/components/counter/counter-time.vue';

export default defineComponent({
  components: { counterTime },
  data() {
    return {
      counters: [{ key: 0 }],
    };
  },

  methods: {
    addCounter() {
      this.counters.push({ key: this.counters.length });
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

@font-face {
  font-family: "Gotham Pro";
  src: local("Gotham Pro"),
  url("@/assets/fonts/gothampro_light.ttf") format("truetype");
}

.app {
  padding: 40px 20px 0 20px;
  width: 100%;
  min-height: 100vh;
  background-color: #E5E5E5;
}

.pageContainer {
  display: flex;
  align-items: start;
  justify-content: center;
  flex-wrap: wrap;
}

.btn {
  display: flex;
  align-content: center;
  justify-content: center;
  flex-wrap: wrap;
  width: 255px;
  height: 120px;
  border: none;
  background-color: #696969;
  cursor: pointer;
  margin: 5px;
}

.cross {
  position: relative;
  width: 20px;
  height: 20px;
}

.line {
  position: absolute;
  height: 100%;
  width: 3px;
  top: 0;
  right: 50%;
  background-color: #9E9E9E;
}

.lineVer {
  transform: rotate(-90deg);
}

</style>
