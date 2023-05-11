<template>
  <div class="dice" :class="{ 'rolling': rolling }" @dice-clicked="roll">
    <svg class="face" :class="'face-' + value" viewBox="0 0 100 100">
      <circle cx="50" cy="50" r="12" v-if="value === 1" />
      <circle cx="30" cy="30" r="12" v-if="[2, 3, 4, 5, 6].includes(value)" />
      <circle cx="70" cy="50" r="12" v-if="[2, 3, 4, 5, 6].includes(value)" />
      <circle cx="30" cy="70" r="12" v-if="[3, 4, 5, 6].includes(value)" />
      <circle cx="70" cy="30" r="12" v-if="[4, 5, 6].includes(value)" />
      <circle cx="30" cy="50" r="12" v-if="[5,6].includes(value)" />
      <circle cx="70" cy="50" r="12" v-if="[6].includes(value)" />
    </svg>
  </div>
</template>

<script>
export default {
  data() {
    return {
      value: 1,
      rolling: false
    };
  },
  methods: {
    roll() {
      // Generate a random number between 1 and 6
      const randomValue = Math.floor(Math.random() * 6) + 1;

      // Set the new value and start the rolling animation
      this.value = randomValue;
      this.rolling = true;
      this.$emit('dice-rolling', this.rolling)
      // Wait for the rolling animation to finish
      setTimeout(() => {
        this.rolling = false;
        this.$emit('dice-rolled', this.value);
      }, 1000);
    }
  }
};
</script>

<style>
.dice {
  display: inline-block;
  width: 100px;
  height: 100px;
  position: relative;
  border-radius: 10px;
  border: 2px solid black;
  overflow: hidden;
  cursor: pointer;
  background: linear-gradient(to bottom, #5c258d, #4389a2, #5c258d);
  background-size: 200% 200%;
  animation: gradient 15s ease infinite;
}
@keyframes gradient {
  0% {
    background-position: 0% 50%;
  }
  50% {
    background-position: 100% 50%;
  }
  100% {
    background-position: 0% 50%;
  }
}
.dice.rolling {
  animation: rolling 1s linear infinite;
}

.dice .face {
  position: relative;
  width: 100%;
  height: 100%;
  transform: translateX(0);
  transition: transform 1s;
}

.dice .face circle {
  fill: black;
}

.dice .face-1 circle:nth-of-type(1) {
  cx: 50;
  cy: 50;
}

.dice .face-2 circle:nth-of-type(1) {
  cx: 30;
  cy: 30;
}

.dice .face-2 circle:nth-of-type(2) {
  cx: 70;
  cy: 70;
}

.dice .face-3 circle:nth-of-type(1) {
  cx: 30;
  cy: 30;
}

.dice .face-3 circle:nth-of-type(2) {
  cx: 50;
  cy: 50;
}

.dice .face-3 circle:nth-of-type(3) {
  cx: 70;
  cy: 70;
}

.dice .face-4 circle:nth-of-type(1) {
  cx: 30;
  cy: 30;
}

.dice .face-4 circle:nth-of-type(2) {
  cx: 70;
  cy: 70;
}

.dice .face-4 circle:nth-of-type(3) {
  cx: 30;
  cy: 70;
}

.dice .face-4 circle:nth-of-type(4) {
  cx: 70;
  cy: 30;
}

.dice .face-5 circle:nth-of-type(1) {
  cx: 30;
  cy: 30;
}

.dice .face-5 circle:nth-of-type(2) {
  cx: 70;
  cy: 70;
}

.dice .face-5 circle:nth-of-type(3) {
  cx: 50;
  cy: 50;
}

.dice .face-5 circle:nth-of-type(4) {
  cx: 70;
  cy: 30;
}

.dice .face-5 circle:nth-of-type(5) {
  cx: 30;
  cy: 70;
}

.dice .face-6 circle:nth-of-type(1) {
  cx: 30;
  cy: 30;
}

.dice .face-6 circle:nth-of-type(2) {
  cx: 70;
  cy: 70;
}

.dice .face-6 circle:nth-of-type(3) {
  cx: 30;
  cy: 50;
}

.dice .face-6 circle:nth-of-type(4) {
  cx: 70;
  cy: 50;
}

.dice .face-6 circle:nth-of-type(5) {
  cx: 30;
  cy: 70;
}

.dice .face-6 circle:nth-of-type(6) {
  cx: 70;
  cy: 30;
}

@keyframes rolling {
  0% {
    transform: translateX(0);
  }
  25% {
    transform: translateX(-25%);
  }
  50% {
    transform: translateX(25%);
  }
  75% {
    transform: translateX(-25%);
  }
  100% {
    transform: translateX(0);
  }
}
</style>
