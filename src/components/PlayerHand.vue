<script setup>
import { ref } from 'vue';
import GameCard from './GameCard.vue';

const numCards = ref(5);
const cardIdRef = ref(6);

const cardNames = ["AppleBug", "Babysnakes", "Bananakeet", "Blobbyfish", "PippyChicken", "PocketBat", "SaladSlug", "Squiddy", "StinkMink", "TurtleBunny"];

const playerHand = ref([
  { petName: "Bananakeet", type: "creature", id: 1 },
  { petName: "Babysnakes", type: "creature", id: 2 },
  { petName: "AppleBug", type: "creature", id: 3 },
  { petName: "PocketBat", type: "creature", id: 4 },
  { petName: "TurtleBunny", type: "creature", id: 5 }
]);

function drawCreatureCard() {
  const newCard = { petName: generateRandomCreatureCard(), type: "creature", id: cardIdRef.value++ };
  numCards.value++;
  playerHand.value.push(newCard);
}

function discardLastCard() {
  numCards.value--;
  playerHand.value.pop();
}

function generateRandomCreatureCard() {
  const randomIdx = Math.floor(Math.random() * cardNames.length)
  return cardNames[randomIdx];
}
</script>

<template>
  <div id="player-hand">
    <button @click="discardLastCard">Discard</button>
    <button @click="drawCreatureCard">Draw</button>
    <p>The player's hand contains {{ numCards }} cards.</p>
    <GameCard v-for="card in playerHand" :key="card.id" :pet-name="card.petName" :card-type="card.type" />
  </div>
</template>

<style scoped>
#player-hand {
  position: absolute;
  text-align: center;
  width: inherit;
  bottom: 10px;
}

button {
  border: 2px solid #fff;
  margin: 5px;
  padding: 5px;
}
</style>
