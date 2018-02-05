<template>
  <div class="row">
    <div class="row">
      <div class="four columns offset-by-four">
        <div class="flip-container" v-bind:class="{ flip: state.selected }">
          <div class="flipper">
            <img class="front" src="../assets/back.png">
            <img id="card" class="back" src="../assets/pa.png">
          </div>
        </div>
      </div>
    </div>
    <div class="row">
      <div class="six columns offset-by-three">
        <h1>Select a card</h1>
      </div>
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
      this.state.selected=index;
    }
  },
  data() {
    return {
      state: { selected: 0, enemy: 0 }
    };
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
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
