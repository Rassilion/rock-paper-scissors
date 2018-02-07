<template>
  <div class="row">
    <div class="row">
      <div class="four columns offset-by-four">
        <div class="flip-container" v-bind:class="{ flip: state.selected }">
          <div class="flipper">
            <img class="front" src="../assets/back.png">
            <img id="card" class="back" v-bind:src="enemyImg">
          </div>
        </div>
      </div>
    </div>
    <div class="row">
      <transition name="fade" mode="out-in">
        <div v-if="!state.selected" key="start" class="six columns offset-by-three">
          <h1>Select a card</h1>
        </div>
        <div v-else key="end" class="eight columns offset-by-two">
          <h1>You {{ state.result }}. Play again?</h1>
        </div>
      </transition>
    </div>
    <div class="row">
      <div class="four columns">
        <img src="../assets/ro.png" @click="selectCard(1)">
      </div>
      <div class="four columns">
        <img src="../assets/pa.png" @click="selectCard(2)">
      </div>
      <div class="four columns">
        <img src="../assets/sc.png" @click="selectCard(3)">
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Game",
  methods: {
    selectCard(index) {
      this.state.selected = index;
      // select enemy card
      this.state.enemy = Math.floor(Math.random() * 3) + 1;
      switch (this.state.enemy) {
        case 1:
          this.enemyImg = require("../assets/ro.png");
          break;
        case 2:
          this.enemyImg = require("../assets/pa.png");
          break;
        case 3:
          this.enemyImg = require("../assets/sc.png");
          break;
      }
      // game logic
      this.state.result = "win";
    }
  },
  data() {
    return {
      enemyImg: null,
      state: { selected: 0, enemy: 0, result: "" }
    };
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter,
.fade-leave-to {
  opacity: 0;
}
/* https://davidwalsh.name/css-flip */
/* entire container, keeps perspective */
.flip-container {
  perspective: 1000px;
}
/* flip the pane when hovered 
.flip-container:hover .flipper,
.flip-container.hover .flipper {
  transform: rotateY(180deg);
}
*/
.flip-container,
.front,
.back {
  width: 131px;
  height: 224px;
}

/* flip speed goes here */
.flipper {
  transition: 0.6s;
  transform-style: preserve-3d;

  position: relative;
}

/* hide back of pane during swap */
.front,
.back {
  backface-visibility: hidden;

  position: absolute;
  top: 0;
  left: 0;
}

/* front pane, placed above back */
.front {
  z-index: 2;
  /* for firefox 31 */
  transform: rotateY(0deg);
}

/* back, initially hidden pane */
.back {
  transform: rotateY(180deg);
}

.flip-container.flip .flipper {
  transform: rotateY(180deg);
}
</style>
