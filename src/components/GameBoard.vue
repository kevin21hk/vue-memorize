<template>
<div class='board'>
<h1>Memorize</h1>
<div class="btn-container">
<button id="btnStart" class="btnStart" @click='start'>
    Start
</button>
<button id="btnFlip" class="btnFlip" @click='flipCards'>
    Flip Cards
</button>
</div>
<div id="gameMsg">
  <p>This simple game tests your memory</p>
</div>
<div class = "card-container" v-if="showCards">
    <template v-for="card in deck.slice(0,5)" :key="card.id">
        <CardDisplay 
        :SpriteX="card.spriteX"    
        :SpriteY="card.spriteY"
        :flipped="card.flipped"
        @click="toggleCardFlip(card)"
        ></CardDisplay>
    </template>
</div>
</div>
</template>

<script>
import CardDisplay from './CardDisplay.vue'
export default {
name: 'GameBoard',
data() {
    return{
        deck : [],
        deck2D : [],
        SpriteX : 0,
        SpriteY : 0,
        showCards: false,
    }
},
components:{
    CardDisplay
},

created(){
    this.initiateNewDeck()
    this.shuffle();
},
methods : {
initiateNewDeck() {
// initialize new deck of cards.

    const suits = ['Spades','Clubs','Hearts','Diamonds']
    const ranks = ['Ace', '2', '3', '4', '5', '6', '7', '8', '9', '10', 'Jack', 'Queen', 'King']
    const cardX = 71
    const cardY = 96
    let id = 1

for (let suitIndex = 0; suitIndex < suits.length; suitIndex++){
    for (let rankIndex = 0; rankIndex < ranks.length; rankIndex++){

    const card = {
        suit : suits[suitIndex],
        rank : ranks[rankIndex],
        value : rankIndex + 1,
        id,
        spriteX : rankIndex * cardX,
        spriteY : suitIndex * cardY,
        spriteXOld : rankIndex * cardX,
        spriteYOld : suitIndex * cardY,
        flipped : false
    }
    this.deck.push(card)
    id++
    }
}
    this.createDeck2D()
},
toggleCardFlip(card) {

  const flippedSpriteX = 213; // Set the flipped sprite X position
  const flippedSpriteY = 480; // Set the flipped sprite Y position

  card.flipped = !card.flipped;

  if (card.flipped) {
        card.spriteX = flippedSpriteX;
        card.spriteY = flippedSpriteY;
    } else {
        card.spriteX = card.spriteXOld;
        card.spriteY = card.spriteYOld;
  }
},
shuffle(){
    for (let i = this.deck.length - 1; i > 0; i--){
    const rand = Math.floor(Math.random() * (i+1));
    [this.deck[i], this.deck[rand]] = [this.deck[rand], this.deck[i]];
    }
},
flipCards() {
    this.deck.slice(0, 5).forEach((card) => {
    card.flipped = true;
    card.spriteX = 213; // Set the flipped sprite X position
    card.spriteY = 480; // Set the flipped sprite Y position
  });
},
start(){
    this.deck = []
    this.deck2D = []
    this.initiateNewDeck()
    this.shuffle()
    this.showCards = true
    document.getElementById('gameMsg').innerText = 
    `Remember the cards, then press the flip button and try guess what each card is, click a card to reveal`
    document.getElementById("btnStart").textContent = `New Game`;
},
createDeck2D()
{
 //create 2d array 4 rows 13 columns
    const rows = 4
    const cols = 13
    this.deck2D = [] 

for (let i = 0; i < rows; i++) {
    const row = this.deck.slice(i * cols, i* cols + cols)
    this.deck2D.push(row)
}
}
}
}
</script>

<style scoped>
.board {
    background-color:rgb(3, 65, 6);
    color: yellow;
    width:80vw;
    height: auto;
    display: flex;
    border-style: solid;
    border-width: 5px;
    border-color:rgb(27, 160, 6);
    margin-bottom: 10px;
    border-radius: 10px;
    flex-direction: column;
}
.card-container {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    grid-gap: 10px;
    display: flex;
    flex-wrap: wrap;
    border-style: dashed;
    width: 60vw;
    height: auto;
    justify-content: center;
    margin: auto;
    padding: 20px;
    margin-bottom: 10px;
    border-radius: 10px;
}

.btn-container {
    display: flex;
    justify-content: center;
    flex-direction: column;
    align-items: center;
}

.btnStart{
    margin: 6px; 
}

.btnFlip{
    margin: 6px;
}

#gameMsg{
    margin-top: 20px;
    margin-bottom: 20px;
    padding: 20px;
}
</style>