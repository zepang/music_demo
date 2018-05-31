<template>
  <div class="progress-bar">
    <div class="progress-bar__wrap">
      <div class="progress" @click.stop="progressClick" ref="progress">
        <div class="progress-bar__mask" ref="progressBarMask"></div>
      </div>
      <div
        ref="progressBtnWrap"
        class="progress-btn__wrap"
        style="left: -15px;"
        v-on:touchstart.prevent="touchstart"
        v-on:touchmove.prevent="touchmove"
        v-on:touchend.prevent="touchend">
        <div class="progress-btn"></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      touch: {}
    }
  },
  methods: {
    moveProgress (value) {
      this.$refs.progressBarMask.style.width = `${value}px`
      this.$refs.progressBtnWrap.style.left = `${this.$refs.progressBarMask.offsetWidth - 15}px`
    },
    progressClick (e) {
      this.moveProgress(e.offsetX)
    },
    touchstart (e) {
      this.touch.startX = e.touches[0].pageX
    },
    touchmove (e) {
      let width = e.touches[0].pageX > 0 ? e.touches[0].pageX : 0
      this.moveProgress(width)
    },
    touchend (e) {
      // this.moveProgress(width)
      console.log(e)
    },
  }
}
</script>


<style scoped>
.progress-bar {
  width: 100%;
  height: 30px;

  display: flex;
  align-items: center;
  justify-content: center;

  box-sizing: border-box;
}

.progress-bar__wrap {
  position: relative;
  width: 100%;
}

.progress {
  height: 4px;
  background-color: rgba(0, 0, 0, .5);
  border-radius: 2px;
}

.progress-bar__mask {
  width: 30px;
  height: 100%;
  min-width: 0;
  max-width: 100%;
  border-radius: 2px;
  background-color: #e83628;

  /* transition: width .25s ease; */
}

.progress-btn__wrap {
  width: 30px;
  height: 30px;
  position: absolute;
  top: 50%;
  left: -4px;
  transform: translate(0, -50%);
}

.progress-btn {
  width: 22px;
  height: 22px;
  margin-left: 4px;
  margin-top: 4px;

  border: 6px solid #ffffff;
  background-color: #e83628;
  border-radius: 100%;
  box-sizing: border-box;
  box-shadow: 0px 0px 10px rgba(0, 0, 0, .3);
}
</style>

