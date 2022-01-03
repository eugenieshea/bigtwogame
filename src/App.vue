<template>
  <div id="app">
    <main>
      <div class="interface">
        <div class="interface-main">
          <div class="title">
            Big 2 Calculator
          </div>
          <div class="input">
            <div class="input-card-val">
              Card Value: 
              <span class="input-card-val-box input-card-val-currency">$</span>
              <input @click="this.limitDecimalPlaces" class="input-card-val-box input-card-val-number" placeholder="Enter" v-model.number="cardValue">
              <span class="input-card-val-box input-card-val-minus" @click="cardValue-=0.1">-</span>
              <span class="input-card-val-box input-card-val-add" @click="cardValue+=0.1">+</span>
            </div>
            <div class="input-name">
            </div>
          </div>
          <div class="calculation">
            calculation
          </div>
        </div>

        <div class="interface-divider"></div>

        <div class="interface-history">
          <div class="settings">

          </div>
          <div class="summation">

          </div>
          <div class="history">

          </div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>

export default {
  name: 'app',
  props: {

  },
  data() {
    return {
      cardValue: 0.1,
    };
  },
  watch: {
    cardValue: {
      handler: function() {
        var num = this.cardValue;
        num = num.toFixed(2)
        num = parseFloat(num);
        this.cardValue = num;
      },
      deep: true
    }
  }
};
</script>

<style>

#app {
  font-family: 'Lato', sans-serif;
  margin: 0;
  background-image: url('https://cdn.wallpapersafari.com/52/82/triKEj.jpg');
  background-size: cover;
  background-position: bottom;
}
main {
  /*
  */
  min-height: 100vh;
  min-width: 100vh; 
  margin: auto;
  /* background-image: linear-gradient(to bottom, rgba(0, 0, 0, 0.25), rgba(0, 0, 0, 0.15)); */
}
.interface {
  display: flex;
  flex-flow: row wrap;
  width: 90%;
  height: 80vh;
  margin: auto;
  padding: 30px;

  border-radius: 10px;
  background-color: rgb(238, 156, 142);
  box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.25);
}
.interface-main {
  display: flex;
  flex-flow: row wrap;
  flex-direction: column;
  height: 100%;
  width: 70%;
  padding: 0;
}
.interface-divider {
  height: 70%;
  margin: auto;
  padding: 2% 0 4% 0;
  border-left: 2px solid white; 
}
.interface-history {
  display: flex;
  flex-flow: row wrap;
  height: 100%;
  width: 29%;
  background-color: blue;
  padding: 0;
}
.title {
  width: 100%;
  flex-grow: 1;
  margin-top: 10px;
  text-align: center;
  font-size: 2em;
}
.input {
  width: 100%;
  flex-grow: 5;
  padding-top: 20px;
  background-color: pink;

  text-align: center;
  font-size: 1.5em;
}
.calculation {
  width: 100%;
  flex-grow: 2;

  background-color: yellow;

  text-align: center;
  font-size: 4em;
}
.input-card-val-box {
  background-color: white;
  font-size: 20px;
  border: 1px solid #ccc;
}
.input-card-val-currency {
  padding: 3px 7px;
  border-radius: 10px 0 0px 10px;
  border-right: none;

}
.input-card-val-number {
  width: 100px;
  text-align: center;
  padding: 3px;
  font-size: 20px;

}
.input-card-val-minus {
  padding: 3px 7px;
  cursor: pointer;
}
.input-card-val-add {
  padding: 3px 7px;
  border-radius: 0 10px 10px 0;
  cursor: pointer;
}

</style>
