<template>
	<div id="app">
            <div class="wrapper clearfix">
            <players 
                v-bind:scorePlayer="scorePlayer" 
                v-bind:activePlayer="activePlayer" 
                v-bind:currentScore="currentScore" 
                v-bind:isWinner="isWinner"
            />
            <controls 
              v-on:handleNewGame="handleNewGame"
              v-on:handleRollDice="handleRollDice"
              v-on:handleHoldScore="handleHoldScore"
              v-bind:finalScore="finalScore"
              v-on:changeFinalScore="changeFinalScore"
              v-bind:isPlaying="isPlaying"
            />
            <dices
               v-bind:dices="dices" 
            />
            <popup-rule
              v-bind:isOpenPopup="isOpenPopup"
              v-on:handleConfirm="handleConfirm"
            />
        </div>
	</div>
</template>

<script>

import  Players from   './components/Players'
import  Controls from  './components/Controls'
import Dices from './components/Dices'
import PopupRule from './components/PopupRule'
export default {
	name: 'app',
	data () {
		return {
            isPlaying:false,
            scorePlayer:[0,0],
            activePlayer:0,
            currentScore : 0,
            isOpenPopup:false,
            dices:[5,5],
            finalScore : 20
		}
	},
	components: {
      Players,
      Controls,
      Dices,
      PopupRule
    },
    computed: {
        
    },
    computed: {
        isWinner(){
            console.log("caallll here");
            let {scorePlayer,finalScore} = this;
            if(scorePlayer[0] >= finalScore ||  scorePlayer[1] >= finalScore){
                this.isPlaying = false;
                return true;
            }
            return false;
        }
    },
    methods: {  
        handleNewGame(){
            this.isOpenPopup = true;
        },

        handleConfirm(){
            this.isPlaying = true;
            this.isOpenPopup = false;
            this.activePlayer = 0;
            this.scorePlayer = [0,0];
            this.currentScore = 0;

        },

        nextPlayer(){
            this.activePlayer = this.activePlayer === 0 ? 1 : 0;
            this.currentScore = 0;
        },

        handleRollDice(){
            if(this.isPlaying){
                var dice1 = Math.floor(Math.random() * 6) + 1;
                var dice2 = Math.floor(Math.random() * 6) + 1;
                this.dices = [dice1,dice2];

                if(dice1 == 1 || dice2 == 1){
                    setTimeout(() => {
                        alert(`Nguoi choi Player ${this.activePlayer + 1} da quay trung so 1.Rat tiec`);
                    },15)
                    this.nextPlayer();
                } else {
                 this.currentScore = this.currentScore + dice1 + dice2;
                }
            } else {
                alert("Vui long nhan vao nut new game");
            }
        },
        handleHoldScore(){
            if(this.isPlaying){
               let { scorePlayer, activePlayer, currentScore} = this;

                let cloneScorePlayer = [...scorePlayer];
               let scoreOld = scorePlayer[activePlayer];
               cloneScorePlayer[activePlayer] = scoreOld + currentScore;
               this.scorePlayer = cloneScorePlayer;
               if(!this.isWinner){
                    this.nextPlayer();
               }
              
            } else {
                 alert("Vui long nhan vao nut new game");
            }
        },
        changeFinalScore(e){
            var number = parseInt(e.target.value);
            if(isNaN(number)){
                this.finalScore = 0;
            } else {
                this.finalScore = number;
            }
        }
    }
}
</script>

<style>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    
}

.clearfix::after {
    content: "";
    display: table;
    clear: both;
}

body {
    background-image: linear-gradient(rgba(62, 20, 20, 0.4), rgba(62, 20, 20, 0.4)), url('/public/assets/back.jpg');
    background-size: cover;
    background-position: center;
    font-family: Lato;
    font-weight: 300;
    position: relative;
    height: 100vh;
    color: #555;
}

.wrapper {
    width: 1000px;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    background-color: #fff;
    box-shadow: 0px 10px 50px rgba(0, 0, 0, 0.3);
    overflow: hidden;
}
</style>
