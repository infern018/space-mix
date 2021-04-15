<template>
  <Modal  v-if="remainingPairs===0" :score="score"/>
  <Modal2 v-if="newPlayer"/>
  <h1> <span>SPACE MIX</span> </h1>
  <transition-group class="game-board" tag="section" name="shuffle-card">
    <Card v-for="card in cardList" :key="`${card.value}-${card.variant}`" :value="card.value" :visible="card.visible" :position="card.position" :matched="card.matched" @select-card="flipCard"/>
  </transition-group>

  <a href="#" class="bar-anchor" @click="startGame" v-if="newPlayer">
     <span>Start</span>
  <div class="transition-bar"></div>
  </a>

  <a href="#" class="bar-anchor" @click="restartGame" v-else>
     <span>Restart</span>
  <div class="transition-bar"></div>
  </a>
</template>

<script>
import _ from 'lodash'
import { computed, ref, watch } from 'vue'
import Card from './components/Card'
import Modal from './components/Modal'
import Modal2 from './components/Modal2'
import { launchConfetti } from './utilties/confetti'

export default {
  name: 'App',
  components:{Card, Modal, Modal2},
  setup(){
    const cardList = ref([])
    const userSelection = ref([])
    const score = ref(0)
    const newPlayer = ref(true)

    const startGame = () => {
      newPlayer.value = false
      restartGame()
    }

    const status = computed(() => {
      if(remainingPairs.value === 0){
        return 'Player Wins'
      } else {
        return `Remaining Pairs : ${remainingPairs.value}`
      }
    })

    const remainingPairs = computed(() => {
      const remainingCards = cardList.value.filter(card => card.matched === false).length;
      return remainingCards/2
    })

    const restartGame = () => {
      cardList.value = _.shuffle(cardList.value)

      cardList.value = cardList.value.map((card, index) => {
        return{
          ...card,
          position:index,
          matched: false,
          visible: false
        }
      })
    }

    const cardItems = [
      '005-comet',
      '008-earth',
      '029-space-shuttle',
      '006-constellations',
      '004-telescope',
      '007-crescent-moon',
      '034-ufo',
      '015-lunar-1'
      ]

    cardItems.forEach(item => {
      cardList.value.push({
        value:item,
        variant:1,
        visible:false,
        position:null,
        matched:false
      })

      cardList.value.push({
        value:item,
        variant:2,
        visible:true,
        position:null,
        matched:false
      })
    })

    cardList.value = cardList.value.map((card, index) => {
      return{
        ...card,
        position:index
      }
    })

    const flipCard = (payload) => {

      score.value+=1
      cardList.value[payload.position].visible = true;

      if(userSelection.value[0]){
        if(userSelection.value[0].position ===  payload.position){
          return
        } else {
          userSelection.value[1] = payload
        }
      } else {
        userSelection.value[0] = payload
      }
    }


    watch(remainingPairs, currentValue => {
      if(currentValue === 0){
        launchConfetti()
      }
    })

    watch(userSelection, currentValue => {
      if(currentValue.length === 2){
        const cardOne = currentValue[0]
        const cardTwo = currentValue[1]

        if(cardOne.faceValue === cardTwo.faceValue){
          cardList.value[cardOne.position].matched = true;
          cardList.value[cardTwo.position].matched = true;
        } else {
          setTimeout(() => {
            cardList.value[cardOne.position].visible = false;
            cardList.value[cardTwo.position].visible = false;
          }, 1000)
          
        }
        userSelection.value.length = 0
      }
    },
    { deep: true })

    return{
      cardList,
      flipCard,
      userSelection,
      status,
      remainingPairs,
      restartGame,
      score,
      newPlayer,
      startGame
    }
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Zen+Dots&display=swap');

body{
  margin:0;
  padding: 0;
  /* background: linear-gradient(to right, #000428, #004e92); */
  background-image: url('../public/images/bg2.jpg');
  background-size: cover;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  color: whitesmoke;
}

h1{
  font-family: 'Zen Dots', cursive;
}

h1 span{
  background-color: rgba(4, 15, 41, 0.9);
  border-radius: 10px;
  border-top-right-radius: 0;
  border-bottom-left-radius: 0;
  padding: 10px 20px;
}

.game-board{
  display:grid;
  grid-template-columns: repeat(4, 100px);
  grid-column-gap: 24px;
  grid-template-rows: repeat(4, 100px);
  grid-row-gap: 24px;
  justify-content: center;
}

.bar-anchor{
  padding: 20px 10px;
  margin:10px 4px;
  color: #fff;
  font-family: 'Zen Dots', cursive;
  text-transform: uppercase;
  text-align: center;
  position: relative;
  text-decoration: none;
  display:inline-block;
   overflow:hidden;
/*    border:1px solid #6098FF; */
}
.bar-anchor span{
  background:rgba(0, 0, 46, 0.8);
  border-radius: 10px;
  width:100%;
  position:relative;
  padding:10px 70px;
   -moz-transition: all .65s cubic-bezier(0.77, 0, 0.175, 1);
  -o-transition: all .65s cubic-bezier(0.77, 0, 0.175, 1);
  -webkit-transition: all .65s cubic-bezier(0.77, 0, 0.175, 1);
  transition: all .65s cubic-bezier(0.77, 0, 0.175, 1);
/*   border:1px solid #6098FF;  */
}
.transition-bar{
    position: absolute;
    top: 0;
    left: 0%;
    width: 0;
    height: 100%;
    background: #80ffd3;
    z-index:-1;
/*     -ms-transform: skewX(-20deg); 
    -webkit-transform: skewX(-20deg); 
    transform: skewX(-20deg); */
}

.bar-anchor:hover .transition-bar{
  width:120%;
  left:110%;
  -moz-transition: all .65s cubic-bezier(0.77, 0, 0.175, 1);
  -o-transition: all .65s cubic-bezier(0.77, 0, 0.175, 1);
  -webkit-transition: all .65s cubic-bezier(0.77, 0, 0.175, 1);
  transition: all .65s cubic-bezier(0.77, 0, 0.175, 1);
}

.shuffle-card-move{
  transition: transform 0.8s ease-in;
}

</style>
