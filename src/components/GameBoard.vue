<template>

<div class='board'>
<h1>Board</h1>
<button @click='shuffle'>
    Shuffle
</button>
<button @click='start'>
    Start
</button>

<div class = "card-container">
<CardDisplay :SpriteX="this.SpriteX" :SpriteY="this.SpriteY"></CardDisplay>
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
        SpriteY : 0
    }
},
components:{
CardDisplay
},

created(){
// initialize deck of cards here.

const suits = ['Spades','Clubs','Hearts','Diamonds']
const ranks = ['Ace', '2', '3', '4', '5', '6', '7', '8', '9', '10', 'Jack', 'Queen', 'King']
const cardX = 71;
const cardY = 96;

for (let suitIndex = 0; suitIndex < suits.length; suitIndex++){
    for (let rankIndex = 0; rankIndex < ranks.length; rankIndex++){

    const card = {

    suit : suits[suitIndex],
    rank : ranks[rankIndex],
    value : rankIndex + 1,

    spriteX : rankIndex * cardX,
    spriteY : suitIndex * cardY

    }
    // console.log(`Card value: ${card.value}, Suit index: ${suitIndex}, Rank index: ${rankIndex}, spriteX: ${card.spriteX}, spriteY: ${card.spriteY}`)

    this.deck.push(card)

    }
}
this.createDeck2D();

},
methods : {
shuffle(){

    for (let i = this.deck.length - 1; i > 0; i--){
    const rand = Math.floor(Math.random() * (i+1));
    [this.deck[i], this.deck[rand]] = [this.deck[rand], this.deck[i]];
    }
    this.createDeck2D();
    console.log(`Deck Shuffled ${JSON.stringify(this.deck2D)}`)

    console.log(`Card value: ${this.deck2D[0][0].value}, spriteX: ${this.deck2D[0][0].spriteX}, spriteY: ${this.deck2D[0][0].spriteY}`)

}
,
start(){
 this.SpriteX = this.deck2D[0][0].spriteX
 this.SpriteY = this.deck2D[0][0].spriteY
 // display first indexes from deck for the time being
 console.log(this.deck2D[0][0])
 
},
createDeck2D()
{
 //create 2d array 4 rows 13 columns

const rows = 4;
const cols = 13;
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
border-width:1px;
border-style:solid;
width:80vw;
height:80vh;
display:flex;
flex-direction:column;
}

.card-container {
    border-style:dashed;
    width: 60vw;
    height: 40vh;
    display:flex;
    justify-content:center;
    margin: auto;
    padding-top:20px;
}


</style>