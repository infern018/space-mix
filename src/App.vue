<template>
  <h1>Flip 'em!</h1>
  <section class="game-board">
    <Card v-for="(card, index) in cardList" :key="`card-${index}`" :value="card"/>
  </section>
</template>

<script>
import Card from './components/Card'

export default {
  name: 'App',
  components:{Card},
  setup(){
    const cardList = []

    for(let i=0; i<16; i++){
      cardList.push(i)
    }

    return{
      cardList
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.game-board{
  display:grid;
  grid-template-columns: 100px 100px 100px 100px;
  grid-column-gap: 30px;
  grid-template-rows: 100px 100px 100px 100px;
  grid-row-gap: 30px;
  justify-content: center;
}

.card{
  border: 5px solid #ccc;
}

</style>
