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
        <div v-else key="end" class="ten columns offset-by-one">
          <h1 @click="playagain()">You {{ state.result }}. Click to play again.</h1>
        </div>
      </transition>
    </div>
    <div class="row">
      <div class="four columns">
        <div class="flip-container" v-bind:class="{ flip: state.selected == 2 || state.selected == 3 }">
          <div class="flipper">
            <img src="../assets/ro.png" @click="selectCard(1)">
            <img class="back" src="../assets/back.png">
          </div>
        </div>
      </div>
      <div class="four columns">
        <div class="flip-container" v-bind:class="{ flip: state.selected == 1 || state.selected == 3 }">
          <div class="flipper">
            <img src="../assets/pa.png" @click="selectCard(2)">
            <img class="back" src="../assets/back.png">
          </div>
        </div>
      </div>
      <div class="four columns">
        <div class="flip-container" v-bind:class="{ flip: state.selected == 2 || state.selected == 1 }">
          <div class="flipper">
            <img src="../assets/sc.png" @click="selectCard(3)">
            <img class="back" src="../assets/back.png">
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Game",
  methods: {
    playagain(){this.state={ selected: 0, enemy: 0, result: "" }},
    selectCard(index) {
      if(this.state.selected!=0){
        return
      }
      this.state.selected = index;
      // select enemy card
      this.state.enemy = Math.floor(Math.random() * 3) + 1;
      switch (this.state.enemy) {
        case 1:
          this.enemyImg = require("../assets/ro.png");
          if (this.state.selected == 1) {
            this.state.result = "Draw";
          } else if (this.state.selected == 3) {
            this.state.result = "Lose";
          } else if (this.state.selected == 2) {
            this.state.result = "Win";
          }
          break;
        case 2:
          this.enemyImg = require("../assets/pa.png");
          if (this.state.selected == 2) {
            this.state.result = "Draw";
          } else if (this.state.selected == 1) {
            this.state.result = "Lose";
          } else if (this.state.selected == 3) {
            this.state.result = "Win";
          }
          break;
        case 3:
          this.enemyImg = require("../assets/sc.png");
          if (this.state.selected == 3) {
            this.state.result = "Draw";
          } else if (this.state.selected == 2) {
            this.state.result = "Lose";
          } else if (this.state.selected == 1) {
            this.state.result = "Win";
          }
          break;
      }
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
