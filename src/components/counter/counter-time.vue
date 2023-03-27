<template>
  <div class="counterBody">
    <div v-bind:class="{ numberWrapper__active: isWork && !isPause, numberWrapper: true }">
      <div class="numberItem">{{ hour ? `${hour}:` : '' }}</div>
      <div class="numberItem">{{ minute ? `${minute}:` : '' }}</div>
      <div class="numberItem">{{ second }}</div>
    </div>
    <div class="btnContainer">
      <button @click="clickButton"
              v-bind:class="{ playBtn: !isWork || isPause,
             pauseBtn: isWork && !isPause, btnWrapper: true  } "/>
      <button @click="reset"
              v-bind:class="{ resetBtn__active: isWork && !isPause, resetBtn: true }"/>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({

  data() {
    return {
      second: 0,
      minute: 0,
      hour: 0,
      isPause: false,
      isWork: false,
    };
  },
  methods: {
    play() {
      this.isPause = false;
      this.isWork = true;
      this.startCounter();
    },

    pause() {
      this.isPause = true;
    },

    reset() {
      this.isWork = false;
      this.isPause = true;
      this.second = 0;
      this.minute = 0;
      this.hour = 0;
    },

    startCounter() {
      const countedSecond = setInterval(() => {
        if (this.isPause) {
          clearTimeout(countedSecond);
        }

        this.second += 1;

        if (this.second === 60) {
          this.second = 0;
          this.minute += 1;
        }

        if (this.minute === 60) {
          this.minute = 0;
          this.hour += 1;
        }

        if (this.hour === 24) {
          this.reset();
        }
      }, 1000);
    },

    clickButton(): void {
      if (this.isWork && !this.isPause) {
        this.pause();
        return;
      }
      this.play();
    },
  },
});
</script>

<style>

.counterBody {
  display: flex;
  align-content: center;
  flex-direction: column;
  width: 255px;
  height: 120px;
  background-color: #696969;
  margin: 5px;
}

.numberWrapper {
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 22px;
  font-family: "Gotham Pro", Helvetica, Arial;
  font-weight: 400;
  height: 50%;
  width: 100%;
  color: #9E9E9E;
  border-bottom: 1px solid #9E9E9E;
  background: inherit;
}

.numberWrapper__active {
  color: #ffffff;
  border-bottom: 1px solid #ffffff;
}

.numberItem {
  background: inherit;
}

.btnContainer {
  height: 50%;
  display: flex;
  align-items: center;
  padding: 0 70px;
  justify-content: space-between;
}

.btnWrapper {
  position: relative;
  width: 20px;
  height: 20px;
  border: none;
  background-color: inherit;
}

.playBtn {
  background: url("@/assets/icon/icon-play.svg") no-repeat;
  cursor: pointer;
}

.resetBtn {
  width: 20px;
  height: 20px;
  background-color: #9E9E9E;
  border: none;
  cursor: pointer;
}

.resetBtn__active {
  background-color: #ffffff;
}

.pauseBtn {
  background: url("@/assets/icon/icon-pause.svg") center no-repeat;
  cursor: pointer;
}

</style>
