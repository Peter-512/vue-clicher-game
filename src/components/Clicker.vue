<template>
  <button @click="decrement(10)">-10</button>
  <button @click="decrement(1)">-1</button>
  Counter: {{ counter }}
  <button @click="increment(1)">+1</button>
  <button @click="increment(10)">+10</button>
  <template v-for="button in newButtons" :key="button.counter"
    ><span @click="increment(button.counter)" v-html="button.button"></span
  ></template>
  <button @click="reverse">Reverse</button>
  <button v-if="counter >= upgradeCosts" @click="upgrade">Upgrade</button>
  <button v-if="counter >= newButtonCosts" @click="newButton">
    New Button
  </button>
</template>

<script>
export default {
  name: "Counter",
  data() {
    return {
      counter: 0,
      countAmount: 1,
      upgradeCosts: 100,
      newButtonCosts: 250,
      newButtons: [],
      buttonCounter: 100,
    };
  },
  methods: {
    decrement(props) {
      this.counter -= props;
    },
    increment(props) {
      this.counter += props;
    },
    reverse() {
      let negative;
      if (this.counter < 0) {
        negative = true;
      }
      this.counter = parseInt(
        this.counter.toString().split("").reverse().join(""),
        10
      );
      if (negative) {
        this.counter *= -1;
      }
    },
    upgrade() {
      this.countAmount *= 5;
      this.counter -= this.upgradeCosts;
      this.upgradeCosts *= 10;
    },
    newButton() {
      this.counter -= this.newButtonCosts;
      this.newButtons.push({
        counter: this.buttonCounter,
        button: "<button>+" + this.buttonCounter + "</button>",
      });
      this.newButtonCosts *= 2;
      this.buttonCounter *= 10;
    },
  },
  mounted() {
    setInterval(() => {
      this.counter += this.countAmount;
    }, 1000);
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
