<template>
  <div class="game-container">
    <div class="road"></div>
    <div class="trees-left" :style="{ backgroundPositionY: `${scrollPosition}px` }"></div>
    <div class="trees-right" :style="{ backgroundPositionY: `${scrollPosition}px` }"></div>
    <div class="time-display">Time: {{ seconds }}s</div>
    <div class="moving-block" :style="{ animationDuration: '5s', width: `${blockSize}px`, height: `${blockSize}px` }"></div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      seconds: 0,
      scrollPosition: 0,
      scrollSpeed: 2,
      blockSize: 50, // Initial size of the block
      intervalId: null,
    };
  },
  mounted() {
    this.startScrolling();
  },
  beforeUnmount() {
    clearInterval(this.intervalId);
  },
  methods: {
    startScrolling() {
      this.intervalId = setInterval(() => {
        this.seconds += 1;
        this.scrollPosition += this.scrollSpeed;
        if (this.scrollPosition >= 100) {
          this.scrollPosition = 0;
        }
        this.blockSize += 10; // Increase the block size over time
      }, 1000); // Update every second
    },
  },
};
</script>

<style scoped>
.game-container {
  position: relative;
  width: 100vw;
  height: 100vh;
  overflow: hidden;
  background-color: #111; /* Dark background */
  color: white; /* Light text color */
}

.road {
  position: absolute;
  left: 50%;
  top: 0;
  width: 50px;
  height: 100vh;
  background: gray;
  transform: translateX(-50%);
  clip-path: polygon(0 0, 100% 0, 60% 100%, 40% 100%);
  z-index: 1;
}

.trees-left, .trees-right {
  position: absolute;
  top: 0;
  width: 200px;
  height: 100%;
  background-color: #333; /* Darker background for trees */
  background-repeat: repeat-y;
}

.trees-left {
  left: 0;
}

.trees-right {
  right: 0;
  background: url('https://www.vectorstock.com/royalty-free-vector/simple-tree-vector-164659') repeat-y;
}

.time-display {
  position: absolute;
  bottom: 10px;
  left: 10px;
  font-size: 24px;
  background: rgba(0, 0, 0, 0.5);
  padding: 10px;
}

.moving-block {
  position: absolute;
  bottom: 0;
  left: 50%;
  background-color: hotpink;
  transform: translateX(-50%);
  animation: moveDown 5s linear infinite, growBlock 5s linear infinite; /* Animate both movement and growth */
}

@keyframes moveDown {
  0% {
    top: 0;
  }
  100% {
    top: 100vh; /* Move to the bottom of the viewport */
  }
}

@keyframes growBlock {
  0% {
    width: 50px; /* Initial size */
    height: 50px; /* Initial size */
  }
  100% {
    width: 100px; /* Final size */
    height: 100px; /* Final size */
  }
}
</style>
