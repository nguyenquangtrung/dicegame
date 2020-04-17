<template>
	<div id="app">
            <div class="wrapper clearfix">
            <players 
                v-bind:scorePlayer="scorePlayer" 
                v-bind:activePlayer="activePlayer" 
                v-bind:currentScore="currentScore" 
            />
            <controls 
              v-on:handleNewGame="handleNewGame"
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
            scorePlayer:[13,30],
            activePlayer:1,
            currentScore : 0,
            isOpenPopup:false,
            dices:[5,5]
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
