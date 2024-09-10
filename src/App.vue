<template>
  <div class="game-container">
    <div class="road"></div>
    <div class="trees-left" :style="{ backgroundPositionY: `${scrollPosition}px` }"></div>
    <div class="trees-right" :style="{ backgroundPositionY: `${scrollPosition}px` }"></div>
    <div class="time-display">Time: {{ seconds }}s</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      seconds: 0,
      scrollPosition: 0,
      scrollSpeed: 2, // Adjust scrolling speed as needed
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
        this.scrollPosition += this.scrollSpeed; // Move forward
        if (this.scrollPosition >= 100) { // Adjust if necessary
          this.scrollPosition = 0; // Reset position
        }
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
}

.road {
  position: absolute;
  left: 0;
  top: 50%;
  width: 100%;
  height: 50px;
  background: gray;
  transform: translateY(-50%);
  rotate: 1;
}

.trees-left, .trees-right {
  position: absolute;
  top: 0;
  width: 200px; /* Adjust width as needed */
  height: 100px;
  background-color: hotpink;}

.trees-left {
  left: 0;
}

.trees-right {
  right: 0;
  background: url('https://www.vectorstock.com/royalty-free-vector/simple-tree-vector-164659') repeat-y; /* Add your tree texture image */
}

.time-display {
  position: absolute;
  bottom: 10px;
  left: 10px;
  font-size: 24px;
  color: white;
  background: rgba(0, 0, 0, 0.5);
  padding: 10px;
}

@keyframes moveDown {
  0% {
    top: 0;
  }
  100% {
    top: 100vh; /* Move to the bottom of the viewport */
  }
}

</style>
