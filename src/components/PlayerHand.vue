<script setup>
import { ref } from 'vue';
import GameCard from './GameCard.vue';

const numCards = ref(5);
const cardIdRef = ref(numCards.value + 1);

const creatureCardNames = ["AppleBug", "Babysnakes", "Bananakeet", "Blobbyfish", "PippyChicken", "PocketBat", "SaladSlug", "Squiddy", "StinkMink", "TurtleBunny"];
const equipmentCardNames = ["PetFood", "RockCandy", "YummyBones"];

const playerHand = ref([
  { petName: "Bananakeet", type: "creature", id: 1 },
  { petName: "Babysnakes", type: "creature", id: 2 },
  { petName: "RockCandy", type: "equipment", id: 3 },
  { petName: "PocketBat", type: "creature", id: 4 },
  { petName: "TurtleBunny", type: "creature", id: 5 }
]);

function drawCard() {
  const isCreatureCard = Math.random() >= 0.25;
  const cardName = generateRandomCard(isCreatureCard);
  const newCard = {};

  if (isCreatureCard) {
    newCard.petName = cardName;
    newCard.type = "creature";
  } else {
    newCard.toolName = cardName;
    newCard.type = "equipment";
  }

  newCard.id = cardIdRef.value++;
  numCards.value++;
  playerHand.value.push(newCard);
}

function generateRandomCard(isCreatureCard) {
  const cardList = isCreatureCard ? creatureCardNames : equipmentCardNames;
  const randomIdx = Math.floor(Math.random() * cardList.length);
  return cardList[randomIdx];
}

function discardLastCard() {
  numCards.value--;
  playerHand.value.pop();
}
</script>

<template>
  <div id="player-hand">
    <button @click="discardLastCard">Discard Last Card</button>
    <button @click="drawCard">Draw Card</button>
    <p>The player's hand contains {{ numCards }} cards.</p>
    <GameCard v-for="card in playerHand" :key="card.id" :pet-name="card.petName" :tool-name="card.toolName"
      :card-type="card.type" />
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
