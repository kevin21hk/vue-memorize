<template>

<div class="card" :style="{'background-position': `-${this.SpriteX}px -${this.SpriteY}px`}">
    <!-- {{ console.log(` spriteX: ${this.SpriteX} and spriteY: ${this.SpriteY}`) }} -->
</div>

</template>

<script>
export default {
name: 'CardDisplay',
props: {
SpriteX: {
    type: Number,
    required: true
},
SpriteY: {
type: Number,
required: true
}


},
data() {
return{

    
}


}


}

</script>

<style>
.card {
background-image: url('../assets/card-sprites.png');
background-position: 0 0;
width: 71px;
height:96px;
border-radius:3px;

}
</style>