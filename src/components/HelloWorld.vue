
<template>
  <div class="dice-container">
    <div class="wager-container">
      <label for="wager-input">Enter your wager:</label>
      <input id="wager-input" type="number" v-model="wager" />
    </div>
    <div class="dice-wrapper">
      <Dice @dice-rolled="handleDiceRolled1" ref="d1" @dice-rolling="handleDiceRolling1"/>
      <Dice @dice-rolled="handleDiceRolled2" ref="d2" @dice-rolling="handleDiceRolling1"/>

    </div>
    <p>
      Your point: {{currentPoint}}
      <button @click="rollDice"> Roll Dice</button>
    </p>
  </div>
</template>

<script>
import Dice from './Dice'
export default {
  name: 'HelloWorld',
  data () {
    return {
      d1: 0,
      d1r: false,
      dr2: false,
      d2: 0,
      pointSet: false,
      point: 0,
      wager: 0
    }
  },
  props: {
    msg: String
  },
  components: {
    Dice
  },
  computed: {
    currentPoint() {
      if (this.d1 === 0 || this.d2 === 0) {
        return 0
      } else {
        return this.point
      }
    }
  },
  methods: {
    rollDice() {
      this.$refs.d1.roll()
      this.$refs.d2.roll()
    },
    setPoint () {
      if (this.d1 !== 0 && this.d2 !== 0) {
      if (!this.pointSet) {
        this.pointSet = true
        this.point = this.d1 + this.d2
        if(this.point === 7 || this.point === 11) {
          alert('YOU WIN')
          this.d1 = 0
          this.d2 = 0
          this.point = 0
          this.pointSet = false
        }
      } else if(this.currentPoint === this.d1 + this.d2) {
          alert('YOU WIN!')
          this.d1 = 0
          this.d2 = 0
          this.point = 0
          this.pointSet = false
        } else if (this.d1 + this.d2 == 7 && (this.d1r == true && this.d2r == true)) {
          alert('YOU LOSE!')
          this.d1 = 0
          this.d2 = 0
          this.point = 0
          this.pointSet = false
        }
      }
    },
    handleDiceRolled1(val) {
      console.log('Dice Rolled: ' + val)

      this.d1 = val
      this.d1r = false
      this.setPoint()
    },
    handleDiceRolled2(val) {
      console.log('Dice Rolled: ' + val)
      this.d2 = val
      this.d2r = false
      this.setPoint()
    },
    handleDiceRolling1(val) {
      console.log('Dice rolling: ' + val)
      this.d1r = true
    },
    handleDiceRolling2(val) {
      console.log('Dice rolling: ' + val)
      this.d22 = true
    }
  }
}
</script>
<style>
.dice-container {
  position: relative;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
}

.wager-container {
  margin-bottom: 2rem;
}

.dice-wrapper {
  position: absolute;
  top: 0;
  left: 50%;
  transform: translateX(-50%);
}
</style>
