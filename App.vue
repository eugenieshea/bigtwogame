<template>
  <div id="app">
    <main>
      <head>
          <meta name="viewport" content="width=device-width, initial-scale=1.0">
      </head>
      <body>
        <div class="interface">
          <div class="interface-main">
            <div class="title">
              BIG 2 CALCULATOR 
            </div>
            <div class="subtitle">
              Hello! 🥸 <br>
              <div class="information">
                <strong>How to use this tool:</strong> <br>
                1. Enter the amount betted on each card. <br>
                2. Enter the player names and their final score <br>
                3. The amount that each player owes/earns will be displayed at the bottom.
              </div>
            </div>
            <div class="input">
              <div class="input-card-val">
                Card Value: 
                <span class="input-card-val-box input-card-val-currency">$</span>
                <input class="input-card-val-box input-card-val-number" @click="this.limitDecimalPlaces" placeholder="Enter" v-model.number="cardValue">
                <span class="input-card-val-box input-card-val-minus" @click="cardValue-=0.1">-</span>
                <span class="input-card-val-box input-card-val-add" @click="cardValue+=0.1">+</span>
              </div>
              <form class="input-player">
                <div class="input-player-box">
                  Player 1: 
                  <input  class="input-player-name" placeholder="Player 1 Name" v-model="players[0].name">	
                  <input class="input-player-score" placeholder="Player 1 Score" v-model="players[0].score">
                </div>
                <div class="input-player-box">
                  Player 2: 
                  <input class="input-player-name" placeholder="Player 2 Name" v-model="players[1].name">	
                  <input class="input-player-score" placeholder="Player 2 Score" v-model="players[1].score">	
                </div>
                <div class="input-player-box">
                  Player 3: 
                  <input class="input-player-name" placeholder="Player 3 Name" v-model="players[2].name">	
                  <input class="input-player-score" placeholder="Player 3 Score" v-model="players[2].score">	
                </div>
                <div class="input-player-box">
                  Player 4: 
                  <input class="input-player-name" placeholder="Player 4 Name" v-model="players[3].name">	
                  <input class="input-player-score" placeholder="Player 4 Score" v-model="players[3].score">	
                </div>
              </form>
            </div>
            <div 
              class="calculation"
              v-if="players[0].score && players[1].score && players[2].score && players[3].score && players[0].name && players[1].name && players[2].name && players[3].name" 
            >
              <div v-for="player in players" :key="player.name">
                <div class="calculation-player">
                  {{ player.name }} 
                  <span class="calculation-lose" v-if="player.owes < 0">owes</span>
                  <span class="calculation-win" v-if="player.owes >= 0">earns</span>
                  ${{ player.owes }}
                </div>
              </div>
            </div>
            <div 
              class="no-calculation"
              v-if="!players[0].score || !players[1].score || !players[2].score || !players[3].score || !players[0].name || !players[1].name || !players[2].name || !players[3].name" >
              Calculations will appear here once all player names and scores have been entered.
            </div>
          </div>
        </div>
      </body>
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
      players: [
        {name: "", score: '', owes: ''}, 
        {name: "", score: '', owes: ''},
        {name: "", score: '', owes: ''},
        {name: "", score: '', owes: ''},
      ],
    };
  },
  watch: {
    cardValue: {
      handler: function() {
        var num = this.cardValue;
        num = num.toFixed(2)
        num = parseFloat(num);
        this.cardValue = num;

        var p1Score = this.players[0].score;
        var p2Score = this.players[1].score;
        var p3Score = this.players[2].score;
        var p4Score = this.players[3].score;

        var p1Owes = ((p2Score-p1Score)+(p3Score-p1Score)+(p4Score-p1Score))*this.cardValue;
        var p2Owes = ((p1Score-p2Score)+(p3Score-p2Score)+(p4Score-p2Score))*this.cardValue;
        var p3Owes = ((p1Score-p3Score)+(p2Score-p3Score)+(p4Score-p3Score))*this.cardValue;
        var p4Owes = ((p1Score-p4Score)+(p2Score-p4Score)+(p3Score-p4Score))*this.cardValue;

        p1Owes = p1Owes.toFixed(2)
        p2Owes = p2Owes.toFixed(2)
        p3Owes = p3Owes.toFixed(2)
        p4Owes = p4Owes.toFixed(2)

        this.players[0].owes = p1Owes;
        this.players[1].owes = p2Owes;
        this.players[2].owes = p3Owes;
        this.players[3].owes = p4Owes;
      },
      deep: true
    },
    players: {
      handler: function() {
        var p1Score = this.players[0].score;
        var p2Score = this.players[1].score;
        var p3Score = this.players[2].score;
        var p4Score = this.players[3].score;

        var p1Owes = ((p2Score-p1Score)+(p3Score-p1Score)+(p4Score-p1Score))*this.cardValue;
        var p2Owes = ((p1Score-p2Score)+(p3Score-p2Score)+(p4Score-p2Score))*this.cardValue;
        var p3Owes = ((p1Score-p3Score)+(p2Score-p3Score)+(p4Score-p3Score))*this.cardValue;
        var p4Owes = ((p1Score-p4Score)+(p2Score-p4Score)+(p3Score-p4Score))*this.cardValue;

        p1Owes = p1Owes.toFixed(2)
        p2Owes = p2Owes.toFixed(2)
        p3Owes = p3Owes.toFixed(2)
        p4Owes = p4Owes.toFixed(2)

        this.players[0].owes = p1Owes;
        this.players[1].owes = p2Owes;
        this.players[2].owes = p3Owes;
        this.players[3].owes = p4Owes;
      },
      deep: true
    },
  }
};
</script>

<style>
:root {
  --primary-dark: rgb(104, 66, 43);
  --primary-light: rgb(223, 191, 166);
  --secondary-light: rgba(223, 191, 166, 0.65);
  --primary-green: rgb(39, 77, 71);
  --primary-red: rgb(182, 80, 57);
  overflow: scroll;
}
::placeholder {
  color: var(--secondary-light);
}

main {
  min-height: 100vh;
  min-width: 100vh; 
  padding: 2%;
  background-color: seashell;
  font-family: 'Inter', sans-serif;
}
.interface {
  display: flex;
  width: 90%;
  height: 80%;
  margin: auto;
  padding: 5%;
  border-radius: 10px;
  box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.25);
  background-color: var(--primary-light);
  color: var(--primary-dark);
}
.interface-main {
  display: flex;
  flex-direction: column;
  height: 100%;
  width: 100%;
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
  padding: 0;
}
.title {
  width: 100%;
  flex-grow: 1;
  margin-top: 10px;
  text-align: center;
  font-size: 40px;
  font-weight: bolder;
  letter-spacing: 3px;
  color: white;
  /* background: salmon; */
}
.subtitle {
  width: 60%;
  margin: auto;
  text-align: center;
  line-height: 200%;
  padding: 2%;
  font-size: 18px;
}
.information {
  border-bottom: 2px solid var(--primary-dark);
  text-align: left;
  padding: 3% 10%;
  font-size: 16px;
}
.input {
  width: 100%;
  flex-grow: 2; /* Not sure if correct */
  padding-top: 2%;
  text-align: center;
  font-size: 14px;
}
.calculation {
  width: 100%;
  flex-grow: 2;
  text-align: center;
}
.input-card-val {
  font-size: 18px;
}
.input-card-val-box {
  background-color: white;
  font-size: 18px;
  border: 1px solid var(--primary-dark);
  vertical-align: middle;
}
.input-card-val-currency {
  padding: 3px 7px;
  border-radius: 10px 0 0px 10px;
  border-right: none;
}
.input-card-val-number {
  width: 80px;
  text-align: center;
  padding: 3px 7px;
  color: rgb(104, 66, 43);
  border-left: none;
}
.input-card-val-minus {
  padding: 3px 7px;
  cursor: pointer;
}
.input-card-val-add {
  padding: 3px 7px;
  cursor: pointer;
  border-radius: 0 10px 10px 0;
}
.input-player {
  padding: 2%;
  margin-top: 10px;
}
.input-player-box {
  padding: 1%;
  font-size: 18px;
}
.input-player-name {
  margin: 10px 30px;
  padding: 3px 7px;
  width: 180px;
  border-radius: 10px;
  background-color: white;
  font-size: 20px;
  border: 1px solid var(--primary-dark);
  color: var(--primary-dark);
}
.input-player-score {
  margin: 10px;
  padding: 3px 7px;
  width: 180px;
  border-radius: 10px;
  background-color: white;
  font-size: 20px;
  border: 1px solid var(--primary-dark);
  color: var(--primary-dark);
}
.calculation-player {
  padding: 1%;
}
.calculation-win {
  color: var(--primary-green);
  font-weight: bolder;
}
.calculation-lose {
  color: var(--primary-red);
  font-weight: bolder;
}
@media screen and (max-width: 530px) {
  ::placeholder {
    font-size: 0.9em;
  }
  .title {
    font-size: 3em;
  }
  .subtitle {
    font-size: 2em;
    padding: 1px;
    margin-left: 0;
    width: 90%;

  }
  .information {
    font-size: 1em;
    width: 100%;
    padding-right: 0;
  }
  .input {
  width: 100%;
  flex-grow: 2; /* Not sure if correct */
  padding-top: 2%;
  font-size: 1.5em;
  }
  .calculation {
    width: 100%;
    flex-grow: 2;
    text-align: center;
    font-size: 1.5em;
  }
  .input-card-val {
    font-size: 1.4em;
  }
  .input-card-val-box {
    font-size: 1.4em;
    vertical-align: middle;
  }
  .input-card-val-currency {
    padding: 3px 7px;
  }
  .input-card-val-number {
    width: 180px;
    text-align: center;
    padding: 3.9px 7px;
  }
  .input-card-val-minus {
    padding: 3px 16px;
  }
  .input-card-val-add {
    padding: 3px 16px;
  }
  .input-player {
    padding: 2%;
    margin-top: 2%;
  }
  .input-player-box {
    padding: 2%;
    font-size: 1.4em;
  }
  .input-player-name {
    width: 300px;
    font-size: 1.4em;
  }
  .input-player-score {
    margin: 2%;
    margin-left: 23%;
    width: 300px;
    font-size: 1.4em;
  }
  .calculation-player {
    padding: 1%;
    font-size: 1.7em;
  }
  .no-calculation {
    font-size: 1.3em;
  }
}
</style>
